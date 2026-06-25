# Sprint 1 — APP Resuelve

## Sprint Goal

El cliente pre-aprobado puede descargar la APP, verificar su identidad, completar
su registro con OTP y enviar su solicitud de línea de crédito en 3 pasos desde el
celular, con mensajes claros si falla la red — sin necesidad de visitar una sucursal
ni contactar a un asesor.

**Capacidad:** 20 pts · **Comprometido:** 20 pts · **Restante en backlog:** 40 pts (Sprints 2–3+)

> **Pre-condicion critica antes de iniciar:** validar el contrato de API del backend
> de Resuelve (OQ-01). Sin contrato confirmado, construir mocks para US-02, US-03
> y US-04 antes del Day 1 del sprint.

---

## Verificacion DoR (gate de entrada al sprint)

Todas las historias incluidas superaron la Definition of Ready:

| Criterio DoR | US-01 | US-02 | US-03 | US-04 | US-05 | US-11 |
|---|---|---|---|---|---|---|
| as_a / want / so_that completos | Sí | Sí | Sí | Sí | Sí | Sí |
| Criterios Gherkin >= 1 | 3 | 4 | 4 | 5 | 4 | 3 |
| Estimacion > 0 y <= 8 pts | 2 | 3 | 5 | 5 | 3 | 2 |
| open_questions vacío | Sí | Sí | Sí | Sí | Sí | Sí |
| **Estado** | **READY** | **READY** | **READY** | **READY** | **READY** | **READY** |

---

## Historias comprometidas

| Historia | Título | Pts | Épica | Prioridad |
|---|---|---|---|---|
| US-01 | Pantalla de bienvenida con video de marca | 2 | EPIC-01 | 1 |
| US-02 | Verificación de cédula y clasificación del flujo | 3 | EPIC-01 | 2 |
| US-03 | Visualización de oferta pre-aprobada y solicitud en 3 pasos | 5 | EPIC-01 | 3 |
| US-04 | Registro de datos personales con validación OTP | 5 | EPIC-01 | 4 |
| US-05 | Creación de contraseña y confirmación de cuenta | 3 | EPIC-01 | 5 |
| US-11 | Mensajes diferenciados de conectividad vs. servicio no disponible | 2 | EPIC-02 | 7 |
| **Total** | | **20 pts** | | |

### Cadena de dependencias del sprint

```
US-01 → US-02 → US-03
                US-04 → US-05
US-11 (sin dependencias — puede desarrollarse en paralelo desde el Day 1)
```

**Ruta critica:** US-01 → US-02 → US-04 → US-05 (13 pts en secuencia).
US-03 (5 pts) y US-11 (2 pts) pueden desarrollarse en paralelo.

---

## Logica de seleccion aplicada

Se seleccionaron historias en orden de prioridad ascendente (1 = mas alta),
verificando en cada paso que todas las dependencias de la historia candidata
estuvieran incluidas en el sprint. La capacidad de 20 pts se distribuyo asi:

| Paso | Historia candidata | Pts | Dep. en sprint | Acum. | Decision |
|---|---|---|---|---|---|
| 1 | US-01 (pri=1) | 2 | — (ninguna) | 2 | ENTRA |
| 2 | US-02 (pri=2) | 3 | US-01 (Sí) | 5 | ENTRA |
| 3 | US-03 (pri=3) | 5 | US-02 (Sí) | 10 | ENTRA |
| 4 | US-04 (pri=4) | 5 | US-02 (Sí) | 15 | ENTRA |
| 5 | US-05 (pri=5) | 3 | US-04 (Sí) | 18 | ENTRA |
| 6 | US-07 (pri=6) | 3 | US-05 (Sí) | 21 > 20 | NO CABE |
| 7 | US-11 (pri=7) | 2 | — (ninguna) | 20 | ENTRA — llena capacidad |
| 8 | US-06 (pri=8) | 3 | — | 23 > 20 | Sprint lleno |

US-07 (Login, 3 pts, prioridad 6) no cabe porque supera la capacidad por 1 pt.
US-11 (2 pts, prioridad 7, sin dependencias) ocupa el margen restante exacto y
aporta robustez transversal al flujo de registro del sprint.

---

## Historias diferidas — backlog refinado (Sprints 2–3+)

| Historia | Pts | Épica | Motivo del diferimiento |
|---|---|---|---|
| US-06 · Estado de solicitud en revisión | 3 | EPIC-01 | Capacidad agotada. Depende de US-05 (en sprint). Candidata Sprint 2. |
| US-07 · Inicio de sesión con cédula y contraseña | 3 | EPIC-02 | No cabe (18 + 3 = 21 pts). Depende de US-05. **Abre Sprint 2 como historia de mayor prioridad.** |
| US-08 · Recuperación de contraseña por correo | 3 | EPIC-02 | Depende de US-07, que no entra en Sprint 1. |
| US-09 · Cierre de sesión | 1 | EPIC-02 | Depende de US-07, que no entra en Sprint 1. |
| US-10 · Aviso y redirección por sesión expirada | 3 | EPIC-02 | Depende de US-07, que no entra en Sprint 1. |
| US-12 · Dashboard con saludo y resumen de crédito | 3 | EPIC-03 | Depende de US-07, que no entra en Sprint 1. |
| US-13 · Estado de cuenta detallado | 3 | EPIC-03 | Depende de US-12, que no entra en Sprint 1. |
| US-14 · Indicador visual de pago próximo | 2 | EPIC-03 | Depende de US-12, que no entra en Sprint 1. |
| US-15 · Gráfico de progreso con niveles de beneficio | 5 | EPIC-04 | Depende de US-13, que no entra en Sprint 1. |
| US-16 · Modal de celebración con premio | 3 | EPIC-04 | Depende de US-15, que no entra en Sprint 1. |
| US-17 · Actualización del nivel en el gráfico | 2 | EPIC-04 | Depende de US-16, que no entra en Sprint 1. |
| US-18 · Notificación push 5 días antes del vencimiento | 5 | EPIC-05 | Depende de US-13, que no entra en Sprint 1. |
| US-19 · Deep link notificación al estado de cuenta | 2 | EPIC-05 | Depende de US-18 y US-13, que no entran en Sprint 1. |
| US-20 · Supresión de notificación si ya pagó | 2 | EPIC-05 | Depende de US-18, que no entra en Sprint 1. |

---

## Notas del Scrum Master

### Impedimento critico: APIs de backend (OQ-01)

El sprint entero depende de que el backend de Resuelve exponga APIs estables para:
verificacion de cedula (US-02), envio de OTP (US-04) y persistencia del registro
(US-05). Esta dependencia esta catalogada como OQ-01 con riesgo alto. El Scrum
Master exige que el equipo valide la disponibilidad y contrato de estas APIs ANTES
del inicio del Sprint 1. Si las APIs no estan disponibles o estables, el equipo
debe construir mocks en la semana previa al sprint para no bloquear la ruta critica.

### US-07 como cuello de botella del backlog total

US-07 (Login) es la dependencia raiz de US-08, US-09, US-10 y en cadena de todas
las epicas EPIC-03, EPIC-04 y EPIC-05. Su postergacion al Sprint 2 implica que
14 de las 20 historias del backlog no pueden entrar hasta que US-07 este terminada.
La Sprint Review del Sprint 1 debe priorizar la apertura del Sprint 2 con US-07
como primera historia, sin excepcion.

### Cuestion abierta a resolver antes del Sprint 2

- OQ-02: proveedor de notificaciones push (FCM / APNs / gateway propio). Sin
  definir antes del Sprint 2, US-18 (5 pts, raiz de EPIC-05) no puede estimarse
  con certeza.
- OQ-03: niveles exactos del grafico de incentivos y umbrales de premio. Sin
  definir antes del Sprint 2, US-15 y US-16 requieren rerefinamiento.
- OQ-04: definicion tecnica de "pago a tiempo" (evento push del backend o polling).
  Determina el diseno de US-16 y US-20.

### Riesgo de evidencia heredada del discovery

El backlog se construyo sobre una sola fuente de entrevista. Las historias de mayor
peso del sprint —US-03 (5 pts, flujo pre-aprobado) y US-04 (5 pts, OTP)— asumen
comportamientos del cliente que deben triangularse con una segunda entrevista antes
o durante el sprint para evitar retrabajos costosos.

### Definition of Done del Sprint

Una historia esta Done cuando:
- Cumple todos los criterios de aceptacion Gherkin definidos en stories.md.
- Pasa revision de codigo (PR aprobado por al menos un miembro del equipo).
- No tiene errores bloqueantes en las plataformas iOS y Android objetivo.
- El flujo fue probado en un dispositivo real (no solo en simulador).
