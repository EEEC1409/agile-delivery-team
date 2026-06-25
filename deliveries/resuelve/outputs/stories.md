# Historias refinadas — APP Resuelve

> **Pasada DoR / INVEST:** Developer + Scrum Master · 2026-06-20
> **Total:** 20 historias · 60 puntos · 0 preguntas abiertas bloqueantes en historias
>
> **Advertencia de evidencia heredada del inbox:** discovery realizado con 1 sola fuente de
> entrevista. Triangular antes de comprometer desarrollo.

---

## Resumen por épica

| Épica | Historias | Puntos | Prioridad |
|---|---|---|---|
| EPIC-01 · Onboarding e Identificación | 6 | 21 pts | 1 |
| EPIC-02 · Autenticación y Sesión | 5 | 12 pts | 2 |
| EPIC-03 · Dashboard y Visibilidad Financiera | 3 | 8 pts | 3 |
| EPIC-04 · Incentivos de Pago | 3 | 10 pts | 4 |
| EPIC-05 · Notificaciones Push | 3 | 9 pts | 5 |
| **Total** | **20** | **60 pts** | — |

---

## EPIC-01 · Onboarding e Identificación de Cliente (21 pts)

---

### US-01 · Pantalla de bienvenida con video de marca   ·   EPIC-01   ·   2 pts
**Como** cliente que instala la APP por primera vez, **quiero** ver la pantalla de bienvenida con el logo y un video de la marca Resuelve, **para** confirmar que estoy en la APP correcta y conocer la marca desde el primer contacto.

Criterios de aceptación (Gherkin):
- Dado que el cliente abre la APP por primera vez, cuando la pantalla carga, entonces se muestra el logo de Resuelve y el video de la marca comienza a reproducirse automáticamente.
- Dado que el video termina o el cliente toca "Continuar", cuando ocurre cualquiera de los dos eventos, entonces la APP avanza a la pantalla de ingreso de cédula.
- Dado que el dispositivo no tiene conexión al abrir la APP, cuando la pantalla de bienvenida carga, entonces el logo se muestra siempre (el video puede omitirse) y el botón "Continuar" está disponible.

Origen: `requisitos.md → R-01`; `user-stories.md → US-01` (Entrevistas_APP_Resuelve.md · US-001)

---

### US-02 · Verificación de cédula y clasificación del flujo   ·   EPIC-01   ·   3 pts
**Como** cliente, **quiero** ingresar mi número de cédula para que la APP identifique si soy cliente Resuelve y me dirija al flujo correcto, **para** no perder tiempo en pantallas que no aplican a mi situación.

Criterios de aceptación (Gherkin):
- Dado que ingreso una cédula válida de cliente Resuelve activo, cuando presiono "Continuar", entonces la APP muestra el flujo de cliente existente.
- Dado que ingreso una cédula de cliente pre-aprobado, cuando presiono "Continuar", entonces la APP muestra el flujo de oferta de crédito.
- Dado que ingreso una cédula no registrada, cuando presiono "Continuar", entonces la APP muestra el flujo de cliente nuevo.
- Dado que ingreso una cédula en lista negra o sin oferta disponible, cuando presiono "Continuar", entonces la APP muestra un mensaje claro sin lenguaje técnico ni mensajes genéricos.

Dependencias: US-01
Origen: `user-stories.md → US-01`; `requisitos.md → R-02, R-04`

---

### US-03 · Visualización de oferta pre-aprobada y solicitud en 3 pasos   ·   EPIC-01   ·   5 pts
**Como** cliente pre-aprobado, **quiero** ver el monto de mi línea de crédito disponible y completar la solicitud en no más de 3 pantallas de ingreso de datos, **para** activar mi crédito sin ir a una sucursal.

Criterios de aceptación (Gherkin):
- Dado que la APP detecta que tengo una oferta pre-aprobada, cuando la pantalla carga, entonces veo el monto de mi línea de crédito antes de iniciar la solicitud.
- Dado que inicio la solicitud, cuando la completo, entonces el proceso no supera 3 pantallas de ingreso de datos.
- Dado que completo los 3 pasos, cuando confirmo, entonces recibo una confirmación visual de que la solicitud fue enviada.
- Dado que tengo una línea de crédito inactiva, cuando ingreso a la APP, entonces veo la capacidad de pago disponible y las opciones de activación.

Dependencias: US-02
Origen: `user-stories.md → US-02`; `requisitos.md → R-03, R-06`; `mvp-canvas.md → Funcionalidades mínimas ítem 2`

---

### US-04 · Registro de datos personales con validación OTP   ·   EPIC-01   ·   5 pts
**Como** cliente en proceso de registro, **quiero** ingresar mis datos personales (nombre, teléfono, correo) y validarlos con un código OTP enviado a mi correo, **para** confirmar mi identidad de forma segura sin depender de un asesor.

Criterios de aceptación (Gherkin):
- Dado que lleno nombre, teléfono y correo válidos, cuando presiono "Siguiente", entonces la APP envía un OTP al correo ingresado en menos de 2 minutos.
- Dado que recibo el OTP, cuando lo ingreso correctamente, entonces la APP avanza al paso de creación de contraseña.
- Dado que el OTP es incorrecto, cuando lo ingreso, entonces la APP muestra un mensaje claro con la opción de reenviar.
- Dado que el OTP expira, cuando intento usarlo, entonces la APP muestra un error y la opción de solicitar uno nuevo.
- Dado que algún campo del formulario es inválido, cuando presiono "Siguiente", entonces la APP muestra un mensaje de error claro y accionable por campo.

Dependencias: US-02
Origen: `user-stories.md → US-03`; `requisitos.md → R-07, R-08, R-11`

---

### US-05 · Creación de contraseña y confirmación de cuenta   ·   EPIC-01   ·   3 pts
**Como** cliente que validó su identidad con OTP, **quiero** crear una contraseña personal que cumpla los requisitos de seguridad y confirmarla, **para** que mi cuenta quede protegida desde el primer uso y mis datos persistan en todos los sistemas integrados de Resuelve.

Criterios de aceptación (Gherkin):
- Dado que ingreso una contraseña con mínimo 8 caracteres, al menos una mayúscula y un número, cuando presiono "Crear cuenta", entonces la APP confirma que la cuenta fue creada.
- Dado que las contraseñas no coinciden en el campo de confirmación, cuando intento continuar, entonces la APP muestra un error antes de intentar guardar.
- Dado que el registro se completa con éxito, cuando la APP persiste los datos, entonces mi información queda disponible en todos los sistemas integrados de Resuelve.
- Dado que ocurre un error al persistir los datos, cuando la APP lo detecta, entonces muestra un mensaje claro con instrucciones de qué hacer (reintentar o contactar soporte).

Dependencias: US-04
Origen: `user-stories.md → US-04`; `requisitos.md → R-09, R-10, R-11`

---

### US-06 · Consulta del estado de solicitud en revisión   ·   EPIC-01   ·   3 pts
**Como** cliente con solicitud enviada, **quiero** ver el estado actual de mi trámite con una etiqueta clara (En revisión, Aprobado, Requiere acción), **para** saber si debo esperar o si hay algo concreto que debo hacer de mi parte.

Criterios de aceptación (Gherkin):
- Dado que inicio sesión con una solicitud en revisión, cuando entro a la APP, entonces veo el estado con una etiqueta clara: "En revisión", "Aprobado" o "Requiere acción".
- Dado que el estado es "Requiere acción", cuando lo veo, entonces aparece un botón o instrucción concreta de qué debo hacer.
- Dado que el estado es "Aprobado", cuando lo veo, entonces la APP me indica el siguiente paso para usar mi línea de crédito.

Dependencias: US-05
Origen: `user-stories.md → US-05`; `requisitos.md → R-05`; `evidence-map.json → pain: incertidumbre-estado-solicitud`

---

## EPIC-02 · Autenticación y Seguridad de Sesión (12 pts)

---

### US-07 · Inicio de sesión con cédula y contraseña   ·   EPIC-02   ·   3 pts
**Como** cliente registrado, **quiero** iniciar sesión ingresando mi cédula y contraseña, **para** acceder a mi información de crédito en menos de 3 segundos.

Criterios de aceptación (Gherkin):
- Dado que ingreso cédula y contraseña correctas, cuando presiono "Ingresar", entonces la APP me lleva al dashboard en menos de 3 segundos.
- Dado que ingreso datos incorrectos, cuando presiono "Ingresar", entonces la APP muestra un mensaje de error claro sin revelar cuál campo específico falló.
- Dado que fallo 5 intentos consecutivos, cuando ocurre el quinto fallo, entonces la APP bloquea temporalmente el acceso e indica el tiempo de espera.

Dependencias: US-05
Origen: `user-stories.md → US-06`; `requisitos.md → R-12`

---

### US-08 · Recuperación de contraseña por correo   ·   EPIC-02   ·   3 pts
**Como** cliente que olvidó su contraseña, **quiero** recuperarla mediante un enlace enviado a mi correo registrado, **para** poder volver a ingresar a la APP sin contactar a un asesor.

Criterios de aceptación (Gherkin):
- Dado que presiono "Olvidé mi contraseña" e ingreso mi correo registrado, cuando confirmo, entonces recibo un enlace de recuperación en menos de 2 minutos.
- Dado que uso el enlace de recuperación, cuando creo una nueva contraseña válida, entonces la APP confirma el cambio y me redirige al login.
- Dado que el enlace de recuperación expiró, cuando intento usarlo, entonces la APP muestra un mensaje claro y la opción de solicitar un nuevo enlace.

Dependencias: US-07
Origen: `user-stories.md → US-07`; `requisitos.md → R-14`

---

### US-09 · Cierre de sesión desde cualquier pantalla   ·   EPIC-02   ·   1 pt
**Como** cliente autenticado, **quiero** cerrar sesión desde cualquier pantalla de la APP, **para** proteger mi información financiera cuando termino de usarla.

Criterios de aceptación (Gherkin):
- Dado que estoy en cualquier pantalla de la APP, cuando accedo al menú y selecciono "Cerrar sesión", entonces mi sesión se invalida en el servidor y soy redirigido a la pantalla de login.
- Dado que cierro sesión, cuando la sesión se invalida, entonces ya no puedo acceder a mis datos financieros sin volver a autenticarme.

Dependencias: US-07
Origen: `requisitos.md → R-15`

---

### US-10 · Aviso y redirección al login por sesión expirada   ·   EPIC-02   ·   3 pts
**Como** cliente autenticado, **quiero** recibir un aviso claro cuando mi sesión expire por inactividad y ser redirigido al login, **para** no perder mi progreso no guardado y saber exactamente qué hacer para volver a entrar.

Criterios de aceptación (Gherkin):
- Dado que mi sesión expira por inactividad, cuando intento realizar cualquier acción, entonces la APP me notifica con un mensaje claro que indica que la sesión expiró.
- Dado que la APP notifica el vencimiento de sesión, cuando confirmo el mensaje, entonces soy redirigido al login sin perder mi progreso no guardado.
- Dado que vuelvo a iniciar sesión tras una expiración, cuando me autentico correctamente, entonces regreso a la sección donde estaba antes de la expiración.

Dependencias: US-07
Origen: `user-stories.md → US-13`; `requisitos.md → R-35`; `evidence-map.json → pain: sesion-expirada-sin-aviso`

---

### US-11 · Mensajes diferenciados de conectividad vs. servicio no disponible   ·   EPIC-02   ·   2 pts
**Como** cliente, **quiero** ver mensajes claros que distingan si el problema es mi conexión a internet o si el servicio de Resuelve no está disponible, **para** no confundir un fallo de la APP con un problema de red y saber qué acción tomar.

Criterios de aceptación (Gherkin):
- Dado que pierdo conexión a internet mientras uso la APP, cuando intento realizar una acción que la requiere, entonces veo un mensaje "Sin conexión a internet", diferenciado visualmente de un error del servicio.
- Dado que hay un error en el servicio de Resuelve, cuando la APP lo detecta, entonces muestra "Servicio no disponible" sin exponer mensajes técnicos ni códigos de error.
- Dado que la conexión o el servicio se restaura, cuando ocurre, entonces la APP permite reintentar la acción sin necesidad de reiniciarla.

Dependencias: ninguna
Origen: `user-stories.md → US-13`; `requisitos.md → R-36, R-41`; `evidence-map.json → pain: confusion-error-conectividad`

---

## EPIC-03 · Dashboard y Visibilidad Financiera (8 pts)

---

### US-12 · Dashboard con saludo personalizado y resumen de crédito   ·   EPIC-03   ·   3 pts
**Como** cliente autenticado, **quiero** ver al ingresar a la APP mi nombre, el saldo disponible de mi línea de crédito y el estado general de mi cuenta, **para** tener una visión inmediata de mi situación financiera sin navegar por múltiples pantallas.

Criterios de aceptación (Gherkin):
- Dado que inicio sesión exitosamente, cuando llego al dashboard, entonces veo mi nombre, el saldo de mi línea de crédito disponible y un indicador del estado general de mi cuenta.
- Dado que tengo un pago próximo, cuando entro al dashboard, entonces el resumen muestra la fecha y el monto mínimo de pago de forma destacada.
- Dado que los datos de mi crédito cargan correctamente, cuando aparecen en pantalla, entonces los montos están formateados en la moneda local (ej. $ 1.200,00).

Dependencias: US-07
Origen: `user-stories.md → US-08`; `requisitos.md → R-16`; `evidence-map.json → pain: desconocimiento-situacion-financiera`

---

### US-13 · Estado de cuenta con cuota al cobro, consumida y fecha mínima   ·   EPIC-03   ·   3 pts
**Como** cliente, **quiero** consultar el detalle de mi estado de cuenta con la cuota al cobro, la cuota consumida y la fecha mínima de pago claramente diferenciadas, **para** planificar mis pagos con información exacta sin llamar a un asesor.

Criterios de aceptación (Gherkin):
- Dado que accedo a la sección de estado de cuenta, cuando la pantalla carga, entonces veo la cuota al cobro, la cuota consumida y la fecha mínima de pago como campos diferenciados con etiquetas claras.
- Dado que hay movimientos recientes en mi cuenta, cuando los veo en el estado de cuenta, entonces aparecen con fecha, descripción breve y monto.
- Dado que no hay movimientos recientes, cuando accedo al estado de cuenta, entonces veo un mensaje que indica que no hay movimientos en el período.

Dependencias: US-12
Origen: `user-stories.md → US-09`; `requisitos.md → R-18`

---

### US-14 · Indicador visual de pago próximo en el dashboard   ·   EPIC-03   ·   2 pts
**Como** cliente con un pago próximo, **quiero** ver la fecha y el monto mínimo de mi próximo pago de forma destacada en el dashboard, **para** actuar antes del vencimiento sin necesidad de entrar a la sección de estado de cuenta.

Criterios de aceptación (Gherkin):
- Dado que tengo un pago con fecha dentro de los próximos 7 días, cuando entro al dashboard, entonces el indicador de pago próximo se muestra en un área destacada con la fecha y el monto.
- Dado que ya pagué antes de la fecha mínima, cuando entro al dashboard, entonces el indicador no muestra alerta de pago pendiente.
- Dado que toco el indicador de pago próximo, cuando navego, entonces la APP me lleva directamente al estado de cuenta con el detalle completo.

Dependencias: US-12
Origen: `user-stories.md → US-08 criterio 2`; `requisitos.md → R-16, R-18`

---

## EPIC-04 · Incentivos de Pago y Motivación (10 pts)

---

### US-15 · Gráfico de progreso con niveles de beneficio   ·   EPIC-04   ·   5 pts
**Como** cliente, **quiero** ver un gráfico con al menos 3 niveles de premio diferenciados que muestre qué beneficio gané y cuál puedo ganar si pago a tiempo, **para** motivarme a pagar antes de la fecha límite con una meta visual concreta.

Criterios de aceptación (Gherkin):
- Dado que accedo a la sección de beneficios, cuando la pantalla carga, entonces veo un gráfico con al menos 3 niveles de premio diferenciados visualmente por comportamiento de pago.
- Dado que mi nivel de pago actual tiene un beneficio ganado, cuando lo veo en el gráfico, entonces puedo distinguir visualmente el beneficio que ya gané del que puedo ganar si pago a tiempo.
- Dado que no he realizado ningún pago aún, cuando veo el gráfico, entonces aparece mi nivel inicial y el beneficio que puedo obtener al pagar por primera vez.

Dependencias: US-13
Origen: `user-stories.md → US-10`; `requisitos.md → R-19`; `evidence-map.json → pain: falta-motivacion-pago`

---

### US-16 · Modal de celebración con premio al pagar a tiempo   ·   EPIC-04   ·   3 pts
**Como** cliente que realizó un pago antes de la fecha mínima, **quiero** recibir un modal de celebración con el nombre y la imagen del premio que gané, **para** sentir que mi buen comportamiento de pago tiene una recompensa concreta y visible.

Criterios de aceptación (Gherkin):
- Dado que el backend confirma un pago realizado antes de la fecha mínima, cuando la APP recibe la confirmación, entonces muestra un modal de celebración con el nombre y la imagen del premio ganado.
- Dado que el modal de celebración aparece, cuando el cliente lo cierra, entonces el modal desaparece y el cliente regresa a la pantalla anterior.
- Dado que el cliente no ha subido de nivel de beneficio con el pago, cuando el pago se procesa, entonces no aparece el modal de celebración.

Dependencias: US-15
Origen: `user-stories.md → US-11`; `requisitos.md → R-20`

---

### US-17 · Actualización del nivel en el gráfico tras recibir el premio   ·   EPIC-04   ·   2 pts
**Como** cliente, **quiero** ver el gráfico de progreso actualizado con mi nuevo nivel al cerrar el modal de celebración, **para** confirmar visualmente que el sistema reconoció mi pago y que mi progreso queda reflejado de inmediato.

Criterios de aceptación (Gherkin):
- Dado que el cliente cierra el modal de celebración, cuando vuelve a ver el gráfico de progreso, entonces el nuevo nivel de beneficio ganado está reflejado en el gráfico.
- Dado que el nivel se actualiza, cuando el cliente vuelve al gráfico, entonces el nivel anterior está visualmente marcado como completado y el siguiente nivel disponible está visible.

Dependencias: US-16
Origen: `user-stories.md → US-11 criterio 2`; `requisitos.md → R-19, R-20`

---

## EPIC-05 · Notificaciones Push de Pago (9 pts)

---

### US-18 · Notificación push con monto y fecha 5 días antes del vencimiento   ·   EPIC-05   ·   5 pts
**Como** cliente con notificaciones push habilitadas, **quiero** recibir una notificación push cuando falten 5 días para mi fecha mínima de pago, con el monto y la fecha, **para** no olvidar pagar y evitar recargos por mora.

Criterios de aceptación (Gherkin):
- Dado que tengo notificaciones push habilitadas y faltan 5 días para mi fecha mínima de pago, cuando llega ese momento, entonces recibo una notificación con el monto exacto y la fecha de vencimiento.
- Dado que ya realicé el pago antes del disparo de la notificación, cuando llega el momento programado, entonces la APP no envía la notificación.
- Dado que recibo la notificación, cuando la veo en la bandeja del sistema operativo, entonces el texto indica claramente el monto y la fecha sin tecnicismos.

Dependencias: US-13
Origen: `user-stories.md → US-12`; `requisitos.md → R-37`; `evidence-map.json → pain: olvido-fecha-pago`

---

### US-19 · Deep link desde la notificación al estado de cuenta   ·   EPIC-05   ·   2 pts
**Como** cliente, **quiero** que al tocar la notificación push de pago la APP se abra directamente en mi estado de cuenta, **para** actuar sobre mi pago en un solo paso sin navegar manualmente.

Criterios de aceptación (Gherkin):
- Dado que recibo la notificación push de pago y la toco, cuando la APP se abre o pasa a primer plano, entonces se muestra directamente la pantalla de estado de cuenta.
- Dado que la APP estaba cerrada cuando toco la notificación, cuando abre, entonces lleva directamente al estado de cuenta sin pasar por el dashboard.
- Dado que mi sesión expiró y toco la notificación, cuando la APP abre, entonces me lleva primero al login y, tras autenticarme, me redirige al estado de cuenta.

Dependencias: US-18, US-13
Origen: `user-stories.md → US-12 criterio 2`

---

### US-20 · Supresión de la notificación cuando el cliente ya pagó   ·   EPIC-05   ·   2 pts
**Como** cliente que ya realizó su pago antes de la fecha límite, **quiero** que la APP no me envíe la notificación de recordatorio si ya pagué, **para** no recibir alertas innecesarias una vez que cumplí con mi obligación.

Criterios de aceptación (Gherkin):
- Dado que el cliente realiza un pago antes del momento programado de la notificación, cuando llega el momento programado, entonces la APP verifica el estado del pago y cancela la notificación automáticamente.
- Dado que la notificación fue cancelada por pago realizado, cuando el cliente abre la APP, entonces no ve ninguna alerta de pago pendiente en el dashboard ni en la bandeja del sistema.

Dependencias: US-18
Origen: `user-stories.md → US-12 criterio 3`
