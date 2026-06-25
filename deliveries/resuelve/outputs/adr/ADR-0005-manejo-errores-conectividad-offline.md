# ADR-0005 · Manejo de errores de conectividad: capa transversal con mensajes diferenciados y sin persistencia offline
**Estado:** aceptado
**Fecha:** 2026-06-24

## Contexto y fuerza

Dos historias de EPIC-02 y un requisito no funcional fuerzan una decision sobre
cómo la APP trata la ausencia de red y los fallos del backend:

- **US-11** (`backlog.json → EPIC-02`) — La APP debe mostrar mensajes que distingan
  "Sin conexión a internet" de "Servicio no disponible", con opción de reintentar
  sin reiniciar el flujo.
- **R-36** (`requisitos.md`) — Mensajes claros y distinguibles cuando no hay
  conexión o los servicios están caídos.
- **R-41** (`requisitos.md`) — Los flujos de error deben ser accionables y
  diferenciados; sin mensajes genéricos que generen confusión.
- **evidence-map.json → pain: `confusion-error-conectividad`** — El cliente no
  distingue si el problema es la APP o la conectividad, generando falsa percepción
  de fallo del producto.

La tension es: ¿cuánta lógica offline vale la pena construir en el MVP? Una APP
completamente offline-first (cache local de saldo, movimientos, estado de cuenta)
reduciría la dependencia de red pero añadiría complejidad de sincronización fuera
del scope del MVP.

## Decisión

Implementar una **capa transversal de interceptores de red** en la APP (React
Native) que:

1. **Detecta el tipo de error antes de mostrarlo al usuario:**
   - Error de red (`Network request failed`, timeout, sin IP) → mensaje
     "Sin conexión a internet. Verifica tu conexión y vuelve a intentarlo."
   - Error HTTP 5xx / servicio caído → mensaje "Servicio temporalmente no
     disponible. Inténtalo en unos minutos."
   - Error HTTP 4xx de negocio → mensaje específico de la operación (ej. "OTP
     incorrecto", "Cédula no encontrada"), nunca un código técnico.

2. **Ofrece una acción de reintento** en la misma pantalla; no fuerza al cliente
   a reiniciar el flujo desde el inicio.

3. **No almacena datos financieros en caché local** para uso offline (saldo,
   cuotas, estado de cuenta). Los datos financieros requieren consistencia en tiempo
   real; una caché obsoleta genera decisiones financieras incorrectas. El MVP no
   incluye historial completo de movimientos (excluido en `mvp-canvas.md → Fuera
   de alcance`), por lo que no hay justificación para persistencia local compleja.

4. **Excepción offline explícita:** la pantalla de bienvenida (US-01) muestra el
   logo siempre (activo en el bundle de la APP) y el video puede omitirse si no
   hay red. Esto no es una decisión de caché de datos, sino de bundle estático.

Esta capa de interceptores se implementa como un módulo `NetworkLayer` transversal
al que todos los módulos funcionales (Onboarding, Auth, Dashboard, Incentivos,
Notificaciones) delegan sus llamadas HTTP.

## Alternativas consideradas

- **Offline-first con SQLite / AsyncStorage como caché de datos financieros** —
  Permitiría mostrar el último saldo conocido sin red. Requiere lógica de
  invalidación de caché, sincronización al volver a tener red y manejo de
  conflictos. No está respaldado por ninguna historia del MVP; `mvp-canvas.md`
  excluye el historial de movimientos. Decisión diferida a V2.

- **Manejo de errores por módulo (sin capa transversal)** — Cada pantalla maneja
  sus propios errores de red de forma independiente. Produce inconsistencia en los
  mensajes (viola R-41) y duplicación de código. Descartado.

- **Notificación en tiempo real del estado de conectividad (banner persistente)** —
  Banner global visible en todas las pantallas cuando no hay red. Añade complejidad
  de estado global (Redux/Context) que no aporta valor diferencial sobre un mensaje
  contextual en el momento de la acción. Puede considerarse en V2.

## Consecuencias

**Ganamos:**
- Cumplimiento de R-36, R-41 y US-11 con un patrón simple y reutilizable.
- El cliente distingue siempre si el problema es su red o el servicio de Resuelve,
  eliminando la falsa percepción de fallo de la APP
  (`evidence-map.json → pain: confusion-error-conectividad`).
- Mensajes de reintento en contexto: el cliente no pierde el flujo donde estaba
  (complementa US-10 que también restaura navegación tras sesión expirada).
- Separación de responsabilidades: los módulos funcionales no mezclan lógica de
  presentación con manejo de red.

**Aceptamos:**
- La APP muestra datos desactualizados si el cliente no tiene red y ya estaba en
  el dashboard (los datos mostrados son los de la última carga exitosa, no hay
  caché persistente). Para el MVP esto es aceptable; el pain primario es la
  confusión, no la falta de datos offline.
- El interceptor debe distinguir los códigos de error del backend de Resuelve (OQ-01);
  si el contrato de API no está definido, la clasificación de errores de negocio
  (4xx) puede ser imprecisa hasta que se valide.
