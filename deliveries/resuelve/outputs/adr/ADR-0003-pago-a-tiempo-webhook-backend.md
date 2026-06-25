# ADR-0003 · Definición técnica de "pagó a tiempo": webhook del backend hacia FCM
**Estado:** aceptado
**Fecha:** 2026-06-20

## Contexto y fuerza

Tres historias del MVP dependen de saber, en tiempo real o casi-real, si el
cliente pagó antes de la fecha mínima:

- **US-16** — Modal de celebración: aparece en la APP cuando el pago se confirma.
- **US-20** — Supresión de notificación: la notificación de recordatorio (US-18)
  no se envía si el cliente ya pagó.
- **US-18** — La notificación programada solo se dispara si el estado de pago
  sigue pendiente a D-5 antes del vencimiento.

Esta es la **OQ-04** del backlog: ¿cómo define el backend técnicamente "pagó a
tiempo" — evento push del backend o polling desde la APP?

La respuesta define si la APP es reactiva (espera que algo le llegue) o proactiva
(pregunta periódicamente al servidor).

## Decisión

**El backend de Resuelve es el emisor del evento de pago.** El flujo es:

1. El Servicio de Pagos de Resuelve confirma un pago antes de la fecha mínima.
2. Emite un evento interno (`payment_confirmed_on_time`) con `{ client_id, amount, level_reached }`.
3. El Webhook / Event Bus llama a la API de FCM con un **data payload push**
   (notificación silenciosa) que lleva `{ type: "payment_confirmed", level: N }`.
4. La APP recibe el push en background/foreground y:
   - Muestra el modal de celebración (US-16).
   - Actualiza el gráfico de progreso (US-17).
   - Cancela el push de recordatorio programado si aún no se envió (US-20).

La APP **no** hace polling al backend para saber si el pago ocurrió.

## Alternativas consideradas

- **Polling desde la APP** — la APP consulta periódicamente el endpoint de estado
  de pago. Simple de implementar, pero consume batería y datos del cliente, y
  añade latencia variable. Además, el discovery describe el modal como una
  notificación de celebración inmediata (`user-stories.md → US-11`), lo que
  sugiere un flujo reactivo, no periódico.
- **WebSocket / conexión persistente** — ofrece tiempo real verdadero pero añade
  complejidad de infraestructura (servidor stateful, reconexión, heartbeat). No
  justificado para un evento de baja frecuencia (un pago por mes por cliente).
- **Push + refresh al abrir la APP** — combinación: la APP también consulta el
  estado al abrir para sincronizar si el push no llegó. Esta es la estrategia de
  **resiliencia complementaria** que se recomienda implementar como mejora en
  Sprint 2, no como MVP.

## Consecuencias

**Ganamos:**
- La APP es reactiva y eficiente: no consume red ni batería en polling.
- El modal de celebración (US-16) aparece oportunamente, reforzando el valor
  emocional del incentivo (`evidence-map.json → pain: falta-motivacion-pago`).
- La supresión de notificación (US-20) puede implementarse con la clave de colapso
  de FCM: el backend envía el push silencioso con `collapse_key: payment_{client_id}`;
  FCM sobreescribe el push de recordatorio si aún no se entregó.

**Aceptamos:**
- Dependencia de que el backend de Resuelve implemente el evento de pago y la
  llamada a FCM. Esto debe acordarse con el equipo técnico de Resuelve como parte
  del contrato de API (OQ-01) antes del Sprint 1.
- Si el push silencioso no llega (red interrumpida), el cliente no verá el modal
  de celebración hasta la próxima apertura de la APP. Aceptable para MVP; la
  resiliencia se mejora en Sprint 2 con consulta de estado al abrir la APP.
- La definición de "subió de nivel de incentivo" (US-16 criterio 3) requiere que
  el payload incluya el nivel anterior y el nuevo. El contrato de evento debe
  especificarlo.
