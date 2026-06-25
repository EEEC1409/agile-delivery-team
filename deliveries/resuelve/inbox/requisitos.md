# Requisitos Candidatos — APP Resuelve

> Todos los requisitos tienen como fuente: `Entrevistas_APP_Resuelve.md`
> Organizados por módulo funcional.

---

## Onboarding e identidad de marca

- **[R-01]** La APP debe mostrar una pantalla de bienvenida con logo y video de la marca Resuelve al primer inicio.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-001 · Cliente Resuelve

- **[R-02]** La APP debe verificar si el usuario es cliente Resuelve mediante su número de cédula y determinar el flujo correspondiente.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-002 · Cliente Resuelve

- **[R-03]** La APP debe mostrar la oferta de línea de crédito al cliente pre-aprobado y permitirle continuar la solicitud en 3 pasos.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-003 · Cliente Resuelve (pre-aprobado)

- **[R-04]** La APP debe mostrar un mensaje claro de rechazo cuando el cliente no califica, sin generar confusión ni frustración.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-004 · Cliente Resuelve

- **[R-05]** La APP debe mostrar el estado actual de la solicitud en revisión e indicar si el cliente debe esperar o tomar alguna acción.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-005 · Cliente Resuelve

- **[R-06]** La APP debe mostrar la capacidad de pago disponible y opciones de activación para clientes con línea de crédito inactiva.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-006 · Cliente Resuelve

---

## Registro de cuenta

- **[R-07]** La APP debe permitir al cliente ingresar sus datos personales (nombre, teléfono, correo) para crear su cuenta.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-007 · Cliente Resuelve (nuevo)

- **[R-08]** La APP debe enviar un código OTP al correo del cliente y validarlo para confirmar su identidad durante el registro.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-008 · Cliente Resuelve

- **[R-09]** La APP debe permitir al cliente crear una contraseña personal para acceder a su cuenta de forma segura.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-009 · Cliente Resuelve

- **[R-10]** Al completar el registro, la APP debe persistir los datos del cliente en todos los sistemas integrados garantizando consistencia.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-010 · Sistema

- **[R-11]** La APP debe mostrar mensajes de error claros y accionables cuando algo falle durante el proceso de registro.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-011 · Cliente Resuelve

---

## Autenticación

- **[R-12]** La APP debe permitir inicio de sesión con cédula y contraseña.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-012 · Cliente Resuelve

- **[R-13]** La APP debe soportar autenticación biométrica (Face ID y/o huella dactilar) como alternativa al ingreso con contraseña.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-013 · Cliente Resuelve (frecuente)

- **[R-14]** La APP debe permitir recuperar la contraseña mediante el correo registrado del cliente.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-014 · Cliente Resuelve

- **[R-15]** La APP debe permitir cerrar sesión desde cualquier pantalla.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-015 · Cliente Resuelve

---

## Dashboard y estado de cuenta

- **[R-16]** La APP debe mostrar un saludo personalizado y un resumen del crédito del cliente al ingresar.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-016 · Cliente Resuelve

- **[R-17]** La APP debe permitir al cliente seleccionar el modelo visual de su tarjeta Resuelve.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-017 · Cliente Resuelve

- **[R-18]** La APP debe mostrar el estado de cuenta con cuota al cobro, cuota consumida y fecha mínima de pago.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-018 · Cliente Resuelve

- **[R-19]** La APP debe mostrar un gráfico de progreso que evidencie qué beneficios y premios puede obtener el cliente según su comportamiento de pago.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-019 · Cliente Resuelve

- **[R-20]** La APP debe notificar visualmente al cliente cuando gana un premio por pagar a tiempo.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-020 · Cliente Resuelve

- **[R-21]** La APP debe mostrar el historial de movimientos del cliente (consumos y notas de crédito).
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-021 · Cliente Resuelve

---

## Puntos y programa de canje

- **[R-22]** La APP debe mostrar el saldo de puntos vigentes del cliente.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-022 · Cliente Resuelve

- **[R-23]** La APP debe mostrar el historial detallado de puntos recibidos y redimidos.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-023 · Cliente Resuelve

- **[R-24]** La APP debe permitir al cliente explorar el catálogo de productos disponibles para canje.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-024 · Cliente Resuelve

- **[R-25]** La APP debe permitir usar puntos para reducir la cuota mensual de un producto en canje.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-025 · Cliente Resuelve

- **[R-26]** La APP debe mostrar el detalle completo de un producto antes de que el cliente confirme el canje.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-026 · Cliente Resuelve

- **[R-27]** La APP debe permitir al cliente confirmar o modificar la dirección de entrega al realizar un canje.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-027 · Cliente Resuelve

- **[R-28]** La APP debe validar en tiempo real la elegibilidad del cliente para completar el canje antes de registrarlo.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-028 · Sistema

- **[R-29]** La APP debe permitir validar la identidad del cliente con Face ID para autorizar el canje.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-029 · Cliente Resuelve

- **[R-30]** La APP debe registrar el canje y enviar confirmación visual y por correo al cliente elegible.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-030 · Cliente Resuelve

- **[R-31]** La APP debe mostrar una explicación clara de los motivos por los que no se puede completar un canje.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-031 · Cliente Resuelve

---

## Perfil y gestión de cuenta

- **[R-32]** La APP debe mostrar todos los datos personales del cliente en un solo lugar para que pueda verificarlos.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-032 · Cliente Resuelve

- **[R-33]** La APP debe permitir al cliente cambiar su contraseña desde el perfil sin necesidad de cerrar sesión.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-033 · Cliente Resuelve

- **[R-34]** La APP debe permitir al cliente eliminar su cuenta mediante un proceso claro y con confirmación explícita.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-034 · Cliente Resuelve

---

## Notificaciones y sesión

- **[R-35]** La APP debe notificar al cliente cuando su sesión expire y redirigirlo automáticamente al login.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-035 · Cliente Resuelve

- **[R-36]** La APP debe mostrar mensajes claros y distinguibles cuando no hay conexión a internet o los servicios están caídos.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-036 · Cliente Resuelve

- **[R-37]** La APP debe enviar notificaciones push al cliente cuando se acerque su fecha de pago.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-037 · Cliente Resuelve

---

## Administración y back-office

- **[R-38]** El back-office debe permitir al administrador gestionar el banner publicitario de la APP sin necesidad de publicar una nueva versión.
  - Tipo: funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-038 · Administrador de negocio

---

## No funcionales

- **[R-39]** La APP debe ser accesible y responder con tiempos de carga aceptables independientemente del dispositivo o capacidades del usuario.
  - Tipo: no funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-039 · Cliente Resuelve

- **[R-40]** La APP debe proteger la información del cliente en todo momento: autenticación segura, sesión con expiración y OTP para operaciones sensibles.
  - Tipo: no funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-008, US-013, US-015, US-029, US-035 · Cliente Resuelve

- **[R-41]** Los flujos de error (registro, canje, conectividad, sesión) deben mostrar mensajes claros, accionables y diferenciados, sin mensajes genéricos que generen confusión.
  - Tipo: no funcional
  - Origen: Entrevistas_APP_Resuelve.md · US-011, US-036 · Cliente Resuelve
