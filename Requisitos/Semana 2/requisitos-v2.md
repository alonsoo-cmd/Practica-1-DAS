
# Requisitos - Semana 1

Documento de requisitos funcionales y de dominio de la Práctica 1 de Diseño y Arquitectura del Software.

**Grupo 4**

**Estado:** Requisitos revisados tras la tutoría del 10 de noviembre de 2026.

## 1. Requisitos funcionales

| ID | Nombre | Descripción |
|---|---|---|
| RF-1 | Discriminación de clientes | El sistema deberá ser capaz de distinguir el tipo de cliente que se conecta a él. |
| RF-2 | Gestión de suscripciones a categorías | El sistema permitirá a los lectores gestionar sus suscripciones a las categorías de noticias disponibles en el periódico digital. |
| RF-2.1 | Alta de suscripción a canales de noticias | El sistema permitirá a los lectores suscribirse a canales de noticias de su interés. |
| RF-2.2 | Baja de suscripción a canales de noticias | El sistema permitirá a los lectores darse de baja de los canales de noticias a los que estén suscritos. |
| RF-3 | Clasificación de noticias | Las noticias serán de política, economía, sociedad, nacionales o internacionales. |
| RF-4 | Pago por suscripción al periódico | El sistema permitirá a los usuarios contratar una suscripción de las diferentes modalidades: trimestral (70 €), semestral (130 €) o anual (190 €). |
| RF-4.1 | Renovación automática | El sistema renovará automáticamente las suscripciones. |
| RF-4.2 | Gestión de pagos fallidos | Cuando el pago falle, el sistema permitirá tres intentos adicionales para pagar. |
| RF-5 | Módulo de estadísticas | El sistema dispondrá de métricas para administradores y redactores sobre noticias más leídas, tiempo de permanencia, tasas de rebote y conversión de lectores a suscriptores. |
| RF-5.1 | Cálculo de la tasa de rebote | La tasa de rebote se calcula como el porcentaje de usuarios que visitan un sitio web y lo abandonan sin realizar ninguna interacción ni navegar a otra página de la misma web. |

## 2. Requisitos de dominio

| ID | Nombre | Descripción |
|---|---|---|
| RD-1 | Aplicación web | El sistema deberá disponer de un front-end web a través del cual los usuarios puedan acceder a las funcionalidades de la aplicación. |
| RD-2 | Diseño web responsive | El front-end web deberá adaptar su interfaz a los dispositivos PC y tablet. |
| RD-3 | Comunicación HTTP/REST | Las peticiones entre el front-end web y el back-end del sistema deberán realizarse mediante HTTP/REST. |
| RD-4 | Pasarela de pago Stripe | El sistema deberá utilizar Stripe como pasarela de pago para procesar los cobros asociados a las suscripciones. |
| RD-5 | Persistencia en PostgreSQL 19 | El back-end del sistema deberá utilizar dos bases de datos en PostgreSQL 19: una destinada a los datos de los administradores y redactores y otra a los datos de los suscriptores. |
