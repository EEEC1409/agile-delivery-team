# ADR-0004 · Autenticación: JWT con refresh token de corta/larga duración
**Estado:** aceptado
**Fecha:** 2026-06-24

## Contexto y fuerza

El backlog incluye historias de EPIC-02 con requisitos de seguridad específicos que
fuerzan una decisión sobre la estrategia de gestión de sesión:

- **US-07** — Login en < 3 s; bloqueo temporal tras 5 intentos fallidos consecutivos.
- **US-09** — Cierre de sesión desde cualquier pantalla (invalidación inmediata del
  lado del servidor).
- **US-10** — La sesión expira por inactividad; el cliente es redirigido al login y
  regresa a la sección donde estaba.
- **US-19** (EPIC-05) — Si la sesión expiró al tocar una notificación push, la APP
  debe llevar al login y luego al estado de cuenta; requiere que el estado de
  navegación sea recuperable post-autenticación.
- **R-40** (`requisitos.md`) — Autenticación segura, sesión con expiración y OTP
  para operaciones sensibles.

La tensión es entre **stateless** (simple, escalable, sin estado en servidor) y
**stateful** (control total para invalidación inmediata). US-09 exige invalidación
real al hacer logout; un JWT stateless puro no puede invalidarse antes de que
expire. US-10 y US-19 exigen que el estado de navegación sea preservado a través
del ciclo de expiración.

## Decisión

**JWT con dos tokens:**

| Token | Duración | Almacenamiento | Propósito |
|---|---|---|---|
| Access token | 15 minutos | Memoria de la APP (no persistido en disco) | Adjunto a cada petición HTTP al API Gateway |
| Refresh token | 7 días | Secure Storage del dispositivo (Keychain iOS / Keystore Android) | Obtener un nuevo access token sin que el cliente vuelva a hacer login |

**Ciclo de vida:**
1. Login exitoso (US-07) → backend emite `access_token` (15 min) + `refresh_token`
   (7 días).
2. Cada petición lleva el `access_token` en el header `Authorization: Bearer`.
3. Cuando el `access_token` expira, la APP usa el `refresh_token` silenciosamente.
4. **Logout (US-09):** la APP envía el `refresh_token` al backend para invalidarlo
   en una lista negra. El `access_token` expira en ≤ 15 min por sí solo.
5. **Sesión expirada (US-10):** si el `refresh_token` también venció (7 días sin
   actividad), el intento de renovación falla → la APP redirige al login y guarda
   la ruta de destino para restaurarla tras la re-autenticación.
6. **Deep link post-expiración (US-19):** cuando el cliente toca una notificación
   push con la sesión vencida, la APP guarda el destino (`screen: account_status`)
   antes de redirigir al login; tras autenticarse, navega al destino guardado.
7. **Lockout (US-07):** el backend lleva el contador de intentos fallidos por
   `client_id`; no es responsabilidad del JWT. La APP muestra el mensaje de bloqueo
   que devuelve el servidor y desactiva el botón durante el tiempo indicado.

## Alternativas consideradas

- **JWT stateless puro (sin refresh token)** — simple, pero el access token debe
  durar horas para que la sesión sea usable, con lo que el logout no puede
  invalidarlo inmediatamente (US-09 no cumplible). Descartado.
- **Sesión server-side (cookie + session store)** — control total de invalidación,
  pero requiere un session store (Redis o DB) en el backend, añade estado y
  latencia. La APP móvil usa cookies de forma incómoda con REST. Descartado para
  MVP; no hay evidencia de que el backend de Resuelve tenga este patrón.
- **OAuth 2.0 completo con authorization server externo** — adecuado si Resuelve
  federa identidades con proveedores externos. El discovery no menciona SSO ni
  identidades federadas (`requisitos.md → R-12`: login con cédula y contraseña
  propia de Resuelve). Scope innecesario para MVP.

## Consecuencias

**Ganamos:**
- Access token de 15 min: ventana de exposición pequeña si es interceptado.
- Refresh token en Secure Storage: protegido por el enclave seguro del dispositivo
  (Keychain iOS / Keystore Android).
- Logout real (US-09): el refresh token se invalida en el servidor; la sesión no
  puede renovarse aunque alguien tenga el token.
- Experiencia fluida: el cliente no hace login cada 15 min; la renovación es
  transparente gracias al interceptor de red (ADR-0005).
- Navegación recuperable (US-10, US-19): la APP guarda la ruta de destino antes
  de redirigir al login, sin lógica adicional en los módulos funcionales.
- Sin estado adicional en el backend más allá de una lista negra de refresh tokens
  revocados (liviana, puede ser Redis con TTL de 7 días).

**Aceptamos:**
- La lista negra de refresh tokens añade un lookup extra al renovar. Costo mínimo
  con Redis o un store con TTL.
- El access token (15 min) sigue siendo válido tras logout durante esa ventana.
  Riesgo mitigado por la vida corta del token y porque la APP lo descarta en
  memoria al hacer logout.
- El backend de Resuelve debe implementar el endpoint de revocación de refresh
  token. Debe incluirse en el contrato de API (OQ-01) antes del Sprint 1.
- La lógica de guardar la ruta de destino post-expiración (US-10 y US-19) vive
  en el interceptor de autenticación de la APP; debe coordinarse con ADR-0005
  (capa transversal de red) para no duplicar lógica de manejo de sesión.
