# Sprint 1 — APP Resuelve
## Sprint Goal
**El cliente pre-aprobado puede descargar la APP, verificar su cédula, registrarse con OTP y solicitar su línea de crédito en 3 pasos desde el celular, con mensajes claros si falla la red.**

**Capacidad:** 20 pts · **Comprometido:** 20 pts · **Restante en backlog:** 40 pts (Sprints 2–3+)

> **Pre-condición crítica antes de iniciar:** validar el contrato de API del
> backend de Resuelve (OQ-01). Sin contrato confirmado, construir mocks para
> US-02, US-03 y US-04 antes del Day 1 del sprint.

---

## Historias comprometidas

| Historia | Título | Pts | Épica | Prioridad |
|---|---|---|---|---|
| US-01 | Pantalla de bienvenida con video de marca | 2 | EPIC-01 | 1 |
| US-02 | Verificación de cédula y clasificación del flujo | 3 | EPIC-01 | 2 |
| US-03 | Visualización de oferta pre-aprobada y solicitud en 3 pasos | 5 | EPIC-01 | 3 |
| US-04 | Registro de datos personales con validación OTP | 5 | EPIC-01 | 4 |
| US-05 | Creación de contraseña y confirmación de cuenta | 3 | EPIC-01 | 5 |
| US-11 | Mensajes diferenciados de conectividad vs. servicio | 2 | EPIC-02 | 7 |
| **Total** | | **20 pts** | | |

### Cadena de dependencias del sprint

```
US-01 → US-02 → US-03
                US-04 → US-05
US-11 (sin dependencias — puede desarrollarse en paralelo)
```

**Ruta crítica:** US-01 → US-02 → US-04 → US-05 (15 pts en secuencia).
US-03 (5 pts) y US-11 (2 pts) pueden desarrollarse en paralelo.

---

## Decisión de selección

**US-07** (Login · 3 pts · prioridad 6) es la siguiente historia por prioridad pero
**no cabe** en los 2 pts disponibles tras incluir US-01..US-05 (18 pts acumulados).
Se incluye **US-11** (2 pts · prioridad 7 · sin dependencias) que llena exactamente
la capacidad y aporta robustez transversal al flujo de registro.

US-07 abre Sprint 2 como historia de mayor prioridad.

---

## Historias diferidas (Sprints 2–3+)

| Historia | Pts | Épica | Razón de diferimiento |
|---|---|---|---|
| US-07 Inicio de sesión | 3 | EPIC-02 | No cabe (1 pt sobre capacidad). Abre Sprint 2. |
| US-06 Estado de solicitud | 3 | EPIC-01 | Dep: US-05 (en sprint); espera login (US-07) para flujo completo. |
| US-09 Cierre de sesión | 1 | EPIC-02 | Dep: US-07 (Sprint 2). |
| US-08 Recuperación contraseña | 3 | EPIC-02 | Dep: US-07 (Sprint 2). |
| US-10 Sesión expirada | 3 | EPIC-02 | Dep: US-07 (Sprint 2). |
| US-12 Dashboard personalizado | 3 | EPIC-03 | Dep: US-07 (Sprint 2). |
| US-13 Estado de cuenta | 3 | EPIC-03 | Dep: US-12 (Sprint 2–3). |
| US-14 Indicador pago próximo | 2 | EPIC-03 | Dep: US-12 (Sprint 2–3). |
| US-15 Gráfico de progreso | 5 | EPIC-04 | Dep: US-13 (Sprint 3). |
| US-18 Notificación push | 5 | EPIC-05 | Dep: US-13 (Sprint 3). |
| US-16 Modal de celebración | 3 | EPIC-04 | Dep: US-15 (Sprint 3). |
| US-17 Actualización de nivel | 2 | EPIC-04 | Dep: US-16 (Sprint 3). |
| US-19 Deep link notificación | 2 | EPIC-05 | Dep: US-18 + US-13 (Sprint 3). |
| US-20 Supresión notificación | 2 | EPIC-05 | Dep: US-18 (Sprint 3). |

---

## Riesgos del sprint

| Riesgo | Impacto | Mitigación |
|---|---|---|
| OQ-01: API del backend de Resuelve no disponible | Alto — bloquea US-02, US-03, US-04 | Construir mocks antes del Day 1. Validar contrato en semana previa al sprint. |
| OTP por email (US-04): proveedor no configurado | Alto — bloquea registro | Confirmar proveedor de email transaccional antes del sprint. |
| APNs: certificado Apple no configurado | Medio — afecta Sprint 3 (US-18) | Tramitar certificado en Sprint 1 para no bloquear Sprint 3. |
| Flujo de 3 pasos (US-03) genera abandono en pruebas | Medio — afecta métrica de conversión | Validar prototipo con 2–3 usuarios antes de implementar. |

---

## Definition of Done del Sprint

Una historia está **Done** cuando:
- Cumple todos los criterios de aceptación Gherkin definidos en `stories.md`.
- Pasa revisión de código (PR aprobado).
- No tiene errores en las plataformas iOS y Android objetivo.
- El flujo fue probado en un dispositivo real (no solo simulador).
