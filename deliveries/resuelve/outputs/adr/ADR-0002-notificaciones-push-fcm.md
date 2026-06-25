# ADR-0002 · Notificaciones push: FCM como capa unificada para iOS y Android
**Estado:** aceptado
**Fecha:** 2026-06-20

## Contexto y fuerza

El MVP incluye notificaciones push de pago (US-18), deep link desde la notificación
al estado de cuenta (US-19) y supresión de notificación cuando el cliente ya pagó
(US-20). Estas tres historias requieren una infraestructura de push que:

1. Funcione en iOS y Android (porque la plataforma es React Native — ADR-0001).
2. Permita al backend de Resuelve disparar notificaciones desde el evento de
   confirmación de pago (ADR-0003).
3. Soporte cancelación de notificaciones programadas cuando el estado del pago cambia.

Esta es la **OQ-02** identificada en `backlog.json`: el backlog exigía definir el
proveedor antes de comprometer US-18 en sprint.

## Decisión

Usar **Firebase Cloud Messaging (FCM)** como capa unificada de notificaciones push
para iOS y Android.

- La APP registra un FCM device token al iniciar sesión y lo envía al backend de
  Resuelve.
- El backend (Servicio de Pagos / Webhook) llama a la API de FCM para enviar
  notificaciones o cancelar las programadas.
- FCM entrega a APNs en iOS y directamente al dispositivo en Android.

## Alternativas consideradas

- **APNs directo (solo iOS)** — cubre solo la mitad de los dispositivos. Descartado
  porque la APP es cross-platform (ADR-0001).
- **OneSignal u otro proveedor de terceros** — añade una dependencia de proveedor
  SaaS de pago sin ventaja técnica sobre FCM para el volumen del MVP. FCM es
  gratuito en el nivel de uso esperado para la validación.
- **Gateway propio de Resuelve** — requiere construir y operar infraestructura de
  push desde cero. Sin evidencia de que Resuelve ya tenga esto (`mvp-canvas.md →
  Riesgos/supuestos`). Costo desproporcionado para el MVP.
- **SMS como fallback** — útil si el cliente no tiene smartphone con datos, pero el
  discovery asume que los clientes tienen smartphone con datos
  (`mvp-canvas.md → Supuesto 1`). No es MVP.

## Consecuencias

**Ganamos:**
- Abstracción unificada: el backend solo habla con FCM; FCM resuelve la entrega
  a APNs (iOS) y Android sin lógica adicional en el backend.
- Soporte nativo para data payloads: el push puede llevar `{ type: "payment_confirmed" }`
  para que la APP decida qué hacer sin un segundo request (US-16, US-20).
- Cancelación de notificaciones programadas: FCM soporta Topic Messaging y
  cancelación por `message_id` o por colapso de clave, lo que permite implementar
  US-20 (supresión post-pago).
- Sin costo hasta volúmenes de millones de mensajes/mes.

**Aceptamos:**
- Dependencia de Firebase (Google). Si Resuelve tiene restricciones de proveedor
  cloud, debe validarse con el equipo de infraestructura antes del Sprint 1.
- El device token de FCM debe renovarse; la APP debe manejar el callback
  `onTokenRefresh` y actualizar el backend.
- APNs requiere certificado de Apple y configuración en Firebase Console; añade
  un paso de setup inicial en el onboarding técnico del proyecto.
