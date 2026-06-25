# ADR-0001 · Plataforma móvil: React Native para iOS y Android
**Estado:** aceptado
**Fecha:** 2026-06-20

## Contexto y fuerza

El MVP de APP Resuelve debe llegar a clientes en iOS y Android. El discovery
(`mvp-canvas.md → Segmento de usuarios`) define como usuarios a clientes que
tienen smartphone con datos. No se especifica plataforma mayoritaria, por lo que
la APP debe funcionar en ambos sistemas operativos desde el lanzamiento.

El backlog tiene 20 historias (60 pts) que deben validarse con una métrica de
conversión en 7 días. El tiempo de entrega del MVP es la fuerza dominante: no
hay margen para mantener dos bases de código nativas independientes en la primera
iteración.

## Decisión

Usar **React Native** como plataforma de desarrollo cross-platform para iOS y
Android, con una única base de código en TypeScript.

## Alternativas consideradas

- **Nativo iOS + Nativo Android (Swift + Kotlin)** — dos bases de código, el
  doble de tiempo de desarrollo, requiere equipos especializados separados. No
  viable para un MVP de validación rápida.
- **Flutter (Dart)** — madurez creciente, buen rendimiento. Ecosistema de
  librerías financieras y de push notifications más limitado que React Native en
  2026. El talento disponible en mercados latinoamericanos es menor.
- **Web App Progresiva (PWA)** — no soporta push notifications nativas fiables en
  iOS (limitaciones de Safari). Descartada porque US-18/US-19/US-20 son
  funcionalidades MVP críticas.

## Consecuencias

**Ganamos:**
- Una sola base de código para iOS y Android.
- Ecosistema maduro para integración con FCM (push), JWT, formularios, navegación.
- Mayor disponibilidad de talento en la región para React Native + TypeScript.
- Posibilidad de reusar lógica de negocio entre plataformas (validaciones,
  llamadas a API, manejo de tokens).

**Aceptamos:**
- Rendimiento de animaciones complejo (ej. gráfico de progreso US-15) puede
  requerir librerías de animación nativas (Reanimated). Costo controlado.
- Acceso a APIs de sistema operativo (biometría futura) requiere módulos nativos
  o librerías de terceros. No bloqueante para el MVP.
- Debugging en dos plataformas simultáneamente cuando haya bugs específicos de
  plataforma.
