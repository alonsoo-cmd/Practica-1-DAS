
# Requisitos - Semana 2

**Grupo 4**

*Esta versión sustituye y deja sin efecto las versiones 1 y 2 de los requisitos, que se mantienen únicamente como registro de la evolución del proyecto.*

## 1. Requisitos funcionales

| ID | Nombre | Descripción |
|---|---|---|
| RF-1 | Aplicación web | El sistema deberá disponer de un front-end web a través del cual los usuarios puedan acceder a las funcionalidades de la aplicación. |
| RF-2 | Discriminación de clientes | El sistema deberá ser capaz de distinguir el tipo de cliente que se conecta a él (PC y tablet). |
| RF-3 | Suscripción a canales de noticias | El sistema permitirá a los lectores suscribirse a las categorías de noticias disponibles en el periódico digital. |
| RF-4 | Clasificación de noticias | Las noticias serán de política, economía, sociedad, nacionales o internacionales. |
| RF-5 | Pago por suscripción al periódico | El sistema permitirá a los usuarios contratar una suscripción de las diferentes modalidades: trimestral (70 €), semestral (130 €) o anual (190 €). |
| RF-5.1 | Renovación automática | El sistema renovará automáticamente las suscripciones. |
| RF-5.2 | Gestión de pagos fallidos | Cuando el pago falle, el sistema permitirá tres intentos adicionales para pagar. |
| RF-6 | Módulo de estadísticas | El sistema dispondrá de métricas para administradores y redactores sobre noticias más leídas, tiempo de permanencia, tasas de rebote y conversión de lectores a suscriptores. |
| RF-6.1 | Cálculo de la tasa de rebote | La tasa de rebote se calcula como el porcentaje de usuarios que visitan un sitio web y lo abandonan sin realizar ninguna interacción ni navegar a otra página de la misma web. |

## 2. Requisitos de dominio

| ID | Nombre | Descripción |
|---|---|---|
| RD-1 | Comunicación HTTP/REST | Las peticiones entre el front-end web y el back-end del sistema deberán realizarse mediante HTTP/REST. |
| RD-2 | Pasarela de pago Stripe | El sistema deberá utilizar Stripe como pasarela de pago para procesar los cobros asociados a las suscripciones. |
| RD-3 | Persistencia en PostgreSQL 19 | El back-end del sistema deberá utilizar dos bases de datos en PostgreSQL 19: una destinada a los datos de los administradores y redactores y otra a los datos de los suscriptores. |
