# User Stories — APP Resuelve (MVP)

> **Advertencia de evidencia:** generado con 1 sola fuente de entrevista
> (`Entrevistas_APP_Resuelve.md`). El gate de readiness exige 2; se procedió
> con autorización explícita. Triangular con una segunda entrevista antes de
> comprometer desarrollo.

Persona principal: **C. (Cliente Resuelve)** — `primera mano`
Scope MVP: onboarding, autenticación, dashboard financiero, incentivos de pago
y notificaciones. El catálogo de canje, biometría y back-office quedan fuera.

---

## Módulo 1 — Onboarding y registro

---

- **[US-01]** Como cliente nuevo, quiero ingresar mi cédula para que la APP
  identifique si soy cliente Resuelve y me dirija al flujo correcto, para no
  perder tiempo llenando formularios que no aplican a mi situación.
  - Criterios de aceptación:
    - Dado que ingreso una cédula válida de cliente Resuelve, cuando presiono
      "Continuar", entonces la APP muestra el flujo de cliente existente.
    - Dado que ingreso una cédula no registrada, cuando presiono "Continuar",
      entonces la APP muestra el flujo de cliente nuevo.
    - Dado que ingreso una cédula en lista negra, cuando presiono "Continuar",
      entonces la APP muestra un mensaje claro de que no hay oferta disponible,
      sin lenguaje técnico ni mensajes de error genéricos.
  - Fuente: Entrevistas_APP_Resuelve.md · US-002, US-004

---

- **[US-02]** Como cliente pre-aprobado, quiero ver mi oferta de línea de crédito
  y poder completar la solicitud en 3 pasos simples, para activar mi crédito sin
  ir a una sucursal.
  - Criterios de aceptación:
    - Dado que la APP detecta que tengo una oferta pre-aprobada, cuando ingreso
      mi cédula, entonces veo el monto de mi línea de crédito antes de continuar.
    - Dado que inicio la solicitud, cuando la completo, entonces el proceso no
      supera 3 pantallas de ingreso de datos.
    - Dado que completo los 3 pasos, cuando confirmo, entonces recibo una
      confirmación de que la solicitud fue enviada.
  - Fuente: Entrevistas_APP_Resuelve.md · US-003

---

- **[US-03]** Como cliente en proceso de registro, quiero ingresar mis datos
  personales (nombre, teléfono, correo) y validarlos con un código OTP, para
  confirmar mi identidad de forma segura sin depender de un asesor.
  - Criterios de aceptación:
    - Dado que lleno nombre, teléfono y correo válidos, cuando presiono
      "Siguiente", entonces la APP envía un OTP al correo ingresado.
    - Dado que recibo el OTP, cuando lo ingreso correctamente, entonces la APP
      avanza al paso de creación de contraseña.
    - Dado que el OTP es incorrecto o expira, cuando lo ingreso, entonces la APP
      muestra un mensaje claro con opción de reenviar.
  - Fuente: Entrevistas_APP_Resuelve.md · US-007, US-008

---

- **[US-04]** Como cliente que completó la validación de identidad, quiero crear
  una contraseña personal para que mi cuenta quede protegida desde el primer uso.
  - Criterios de aceptación:
    - Dado que ingreso una contraseña que cumple los requisitos de seguridad
      (mínimo 8 caracteres, al menos una mayúscula y un número), cuando presiono
      "Crear cuenta", entonces la APP confirma que mi cuenta fue creada.
    - Dado que las contraseñas no coinciden en el campo de confirmación, cuando
      intento continuar, entonces la APP muestra un error antes de intentar
      guardar.
    - Dado que el registro se completa, cuando la APP persiste mis datos, entonces
      mi información queda disponible en todos los sistemas integrados.
  - Fuente: Entrevistas_APP_Resuelve.md · US-009, US-010, US-011

---

- **[US-05]** Como cliente con solicitud enviada, quiero ver el estado actual de
  mi trámite, para saber si debo esperar o si hay algo que deba hacer de mi parte.
  - Criterios de aceptación:
    - Dado que inicio sesión con una solicitud en revisión, cuando entro a la APP,
      entonces veo el estado actual con una etiqueta clara ("En revisión",
      "Aprobado", "Requiere acción").
    - Dado que el estado es "Requiere acción", cuando lo veo, entonces aparece un
      botón o instrucción concreta de qué debo hacer.
  - Fuente: Entrevistas_APP_Resuelve.md · US-005

---

## Módulo 2 — Autenticación

---

- **[US-06]** Como cliente registrado, quiero iniciar sesión con mi cédula y
  contraseña, para acceder a mi información de crédito de forma rápida.
  - Criterios de aceptación:
    - Dado que ingreso cédula y contraseña correctas, cuando presiono "Ingresar",
      entonces la APP me lleva al dashboard en menos de 3 segundos.
    - Dado que ingreso datos incorrectos, cuando presiono "Ingresar", entonces la
      APP muestra un mensaje de error claro sin revelar cuál campo falló.
    - Dado que fallo 5 intentos consecutivos, cuando ocurre, entonces la APP
      bloquea temporalmente el acceso e indica el tiempo de espera.
  - Fuente: Entrevistas_APP_Resuelve.md · US-012

---

- **[US-07]** Como cliente que olvidó su contraseña, quiero recuperarla mediante
  mi correo registrado, para volver a ingresar sin contactar a un asesor.
  - Criterios de aceptación:
    - Dado que presiono "Olvidé mi contraseña", cuando ingreso mi correo
      registrado, entonces recibo un enlace de recuperación en menos de 2 minutos.
    - Dado que uso el enlace de recuperación, cuando creo una nueva contraseña
      válida, entonces la APP confirma el cambio y me redirige al login.
    - Dado que el enlace expiró, cuando intento usarlo, entonces la APP muestra
      una opción de solicitar uno nuevo.
  - Fuente: Entrevistas_APP_Resuelve.md · US-014

---

## Módulo 3 — Dashboard y estado de cuenta

---

- **[US-08]** Como cliente, quiero ver un saludo personalizado y un resumen de mi
  crédito al ingresar a la APP, para tener una visión inmediata de mi situación
  financiera sin necesidad de navegar por múltiples pantallas.
  - Criterios de aceptación:
    - Dado que inicio sesión exitosamente, cuando llego al dashboard, entonces veo
      mi nombre, el saldo de mi línea de crédito disponible y un indicador del
      estado general de mi cuenta.
    - Dado que tengo un pago próximo, cuando entro al dashboard, entonces el
      resumen muestra la fecha y el monto mínimo de pago de forma destacada.
  - Fuente: Entrevistas_APP_Resuelve.md · US-016

---

- **[US-09]** Como cliente, quiero consultar el detalle de mi estado de cuenta
  (cuota al cobro, cuota consumida, fecha mínima de pago), para planificar mis
  pagos con información exacta.
  - Criterios de aceptación:
    - Dado que accedo a la sección de estado de cuenta, cuando la pantalla carga,
      entonces veo la cuota al cobro, la cuota consumida y la fecha mínima de pago
      claramente diferenciadas.
    - Dado que el estado de cuenta tiene movimientos recientes, cuando los veo,
      entonces aparecen con fecha, descripción y monto.
  - Fuente: Entrevistas_APP_Resuelve.md · US-018

---

## Módulo 4 — Incentivos de pago

---

- **[US-10]** Como cliente, quiero ver un gráfico de progreso que muestre qué
  beneficios puedo obtener según mi comportamiento de pago, para motivarme a
  pagar antes de la fecha límite.
  - Criterios de aceptación:
    - Dado que accedo a la sección de beneficios, cuando la pantalla carga,
      entonces veo un gráfico con al menos 3 niveles de premio diferenciados por
      comportamiento de pago.
    - Dado que mi nivel de pago actual tiene asociado un beneficio, cuando lo
      veo, entonces puedo distinguir el beneficio que ya gané del que puedo ganar
      si pago a tiempo.
  - Fuente: Entrevistas_APP_Resuelve.md · US-019

---

- **[US-11]** Como cliente que pagó a tiempo, quiero recibir una notificación
  visual de celebración con el premio que gané, para sentir que mi buen
  comportamiento tiene recompensa concreta.
  - Criterios de aceptación:
    - Dado que realizo un pago antes de la fecha mínima, cuando el sistema lo
      procesa, entonces aparece un modal de celebración con el nombre y la imagen
      del premio ganado.
    - Dado que el modal de premio aparece, cuando lo cierro, entonces el nuevo
      nivel de beneficio queda reflejado en el gráfico de progreso.
  - Fuente: Entrevistas_APP_Resuelve.md · US-020

---

## Módulo 5 — Notificaciones

---

- **[US-12]** Como cliente, quiero recibir una notificación push cuando se acerque
  mi fecha de pago, para no olvidarme y evitar recargos por mora.
  - Criterios de aceptación:
    - Dado que tengo notificaciones push habilitadas, cuando falten 5 días para
      mi fecha mínima de pago, entonces recibo una notificación con el monto y la
      fecha.
    - Dado que la notificación aparece, cuando la toco, entonces la APP se abre
      directamente en el estado de cuenta.
    - Dado que ya pagué antes de la fecha límite, cuando se dispararía la
      notificación, entonces la APP no la envía.
  - Fuente: Entrevistas_APP_Resuelve.md · US-037

---

## Módulo 6 — Resiliencia y sesión (transversal de calidad)

---

- **[US-13]** Como cliente, quiero que la APP me muestre mensajes claros cuando
  no haya conexión o cuando mi sesión expire, para no pensar que la aplicación
  falló y saber exactamente qué hacer.
  - Criterios de aceptación:
    - Dado que pierdo conexión a internet mientras uso la APP, cuando intento
      realizar una acción que la requiere, entonces veo un mensaje que distingue
      "sin conexión" de "servicio no disponible".
    - Dado que mi sesión expira por inactividad, cuando intento hacer cualquier
      acción, entonces la APP me notifica y me redirige al login sin perder mi
      progreso no guardado.
    - Dado que la APP redirige al login por sesión expirada, cuando vuelvo a
      iniciar sesión, entonces regreso a la sección donde estaba.
  - Fuente: Entrevistas_APP_Resuelve.md · US-035, US-036
