
# Requisitos - Semana 1

Documento de requisitos funcionales y de dominio de la Práctica 1.

## 1. Requisitos funcionales

| ID | Nombre | Descripción |
|---|---|---|
| RF-1 | Discriminación de dispositivos | El sistema deberá ser capaz de distinguir el tipo de cliente que se conecta a él (cliente PC, cliente tablet). |
| RF-2 | Modalidades de pago | El sistema permitirá seleccionar una de las tres modalidades de suscripción disponibles: trimestral (70 €), semestral (130 €) o anual (190 €). |
| RF-2.1 | Renovación automática | El sistema renovará automáticamente las suscripciones que permanezcan activas al finalizar el período contratado, realizando el cobro correspondiente cada 3, 6 o 12 meses según la modalidad contratada. |
| RF-2.2 | Gestión de pagos fallidos | Cuando el pago falle, el sistema permitirá hasta tres intentos adicionales. Si todos fallan, suspenderá los nuevos intentos de pago de esa suscripción durante 24 horas. Transcurrido ese plazo, se podrá iniciar un nuevo proceso de pago. |
| RF-2.3 | Gestión de renovaciones fallidas | Cuando falle el cobro de una renovación automática, el sistema establecerá la suscripción en estado de pago pendiente. Si después de los intentos definidos no funciona, se suspenderán los servicios asociados a la cuenta del usuario hasta que este complete el pago pendiente. |
| RF-3 | Registro de usuarios | El sistema permitirá a los usuarios crear una cuenta personal mediante el registro de sus datos básicos y credenciales de acceso. Cada cuenta permitirá identificar al usuario y asociarle sus suscripciones y operaciones de pago. |
| RF-3.1 | Alta de suscripciones | El sistema permitirá a los usuarios registrados contratar una suscripción de pago seleccionando una de las opciones disponibles. Una vez confirmado el pago, la suscripción quedará asociada a su cuenta y se activará el acceso a los servicios contratados. |
| RF-3.2 | Consulta de suscripción | El sistema permitirá a los usuarios autenticados consultar el estado de su suscripción, la modalidad contratada, su próxima fecha de renovación y el historial de pagos realizados. |
| RF-3.3 | Baja de suscripciones | El sistema permitirá a los suscriptores cancelar su suscripción de pago en cualquier momento. La cancelación impedirá futuros cobros automáticos, manteniendo el acceso del usuario hasta el final del período contratado. |
| RF-4 | Gestión y consulta de noticias | El sistema proporcionará las funcionalidades necesarias para la publicación, clasificación, consulta, búsqueda y filtrado de las noticias del periódico digital. |
| RF-4.1 | Publicación de noticias | El sistema permitirá a los redactores autenticados publicar noticias, indicando al menos titular, contenido, autor, fecha de publicación y clasificación. |
| RF-4.2 | Lectura de noticias | El sistema permitirá a los usuarios con una suscripción de pago activa consultar y visualizar el contenido completo de las noticias publicadas. |
| RF-4.3 | Búsqueda de noticias | El sistema permitirá a los lectores buscar noticias mediante palabras presentes en su titular o contenido. |
| RF-4.4 | Filtrado de noticias | El sistema permitirá a los lectores filtrar las noticias según su categoría temática, zona geográfica, redactor o fecha de publicación. |
| RF-4.5 | Clasificación de noticias | El sistema permitirá clasificar cada noticia mediante una categoría temática (política, economía o sociedad) y una zona geográfica (nacional o internacional). |
| RF-5 | Recogida de estadísticas | El sistema recogerá métricas de uso relativas a las noticias más leídas, tiempo de permanencia, tasa de rebote y conversión de lectores a suscriptores. |
| RF-6 | Visualización de estadísticas | El sistema permitirá a los administradores y redactores consultar, mediante un panel de estadísticas, las métricas recogidas sobre el periódico. |
| RF-7 | Autenticación | El sistema permitirá a los administradores y redactores autenticarse para acceder a las funcionalidades correspondientes a su rol. |
| RF-8 | Gestión de suscripciones a categorías | El sistema permitirá a los lectores gestionar sus suscripciones a las categorías de noticias disponibles en el periódico digital. |
| RF-8.1 | Alta de suscripción a categorías | El sistema permitirá a los lectores suscribirse a las categorías de noticias de su interés. |
| RF-8.2 | Baja de suscripción a categorías | El sistema permitirá a los lectores darse de baja de las categorías de noticias a las que estén suscritos. |

## 2. Requisitos de dominio

| ID | Nombre | Descripción |
|---|---|---|
| RD-1 | Aplicación web | El sistema deberá disponer de un front-end web a través del cual los usuarios puedan acceder a las funcionalidades de la aplicación. |
| RD-2 | Diseño web responsive | El front-end web deberá adaptar su interfaz a los dispositivos PC y tablet. |
| RD-3 | Comunicación HTTP/REST | Las peticiones entre el front-end web y el back-end del sistema deberán realizarse mediante HTTP/REST. |
| RD-4 | Pasarela de pago Stripe | El sistema deberá utilizar Stripe como pasarela de pago para procesar los cobros asociados a las suscripciones. |
| RD-5 | Persistencia en PostgreSQL 19 | El back-end del sistema deberá utilizar dos bases de datos independientes implementadas en PostgreSQL 19: una destinada a los datos de los administradores y redactores y otra a los datos de los suscriptores. |
