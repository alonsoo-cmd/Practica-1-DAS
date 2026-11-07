# Gestión de notificaciones/suscripciones

## Context and Problem Statement

En la aplicación del periódico digital, es necesario que los usuarios puedan suscribirse a noticias, temas o redactores. Para ello, es necesario un mecanismo para poder notificar a todos los usuarios suscritos.

## Decision Drivers

* RF-9
* RF-9.2

## Considered Options

* Patrón Observer
* Patrón Decorator

## Decision Outcome

Chosen option: "Patrón Observer", because el patrón de diseño presenta una solución elegante al problema planteado: permite notificar a un número N de "subscribers" cuando se publique una nueva noticia (publisher) de un tema (economia, politica...) o de un redactor.

### Consequences

* Good, because permite cambiar el estado de las suscripciones de cada uno de los usuarios en tiempo de ejecución (que al ser una aplicacion web, será la gran mayoría de casos).
* Good, because es escalable en ambos sentidos: permite escalar fácilmente el numero de suscriptores y de publishers (añadir un tipo nuevo de publisher que notifique, por ejemplo de noticias de más de X visualizaciones).
* Good, because resulta fácilmente extensible al soportar varios tipos de notificación haciendo que los publishers hereden de una interfaz común (por ejemplo, añadir notificación por SMS) sin alterar código existente.
* Good, because permite fácilmente realizar las operaciones de alta/baja de un usuario (simplemente se elimina al suscriptor correspondiente de la estructura de datos del publisher), al igual que hacer altas y bajas masivas (por ejemplo, por la eliminación de un publisher).

* Bad, because se necesita almacenar información de cada suscriptor en el objeto subscriber y puede interferir con la anonimidad


## Pros and Cons of the Options

### Patrón Decotator

* Good, because permite cambiar el estado de las suscripciones de cada uno de los usuarios en tiempo de ejecución (que al ser una aplicacion web, será la gran mayoría de casos).
* Good, because permite enlazar y desenlazar diferentes tipos de notificadores (los objetos wrapper contienen la lógica de notificación), lo que permite la fácil implementación de más métodos de notificar.

* Bad, because presenta una implementación menos elegante de notificadores combinados (Email-politics-notifier, Sms-politics-notifier, Email-economy-notifier...)
* Bad, because para cada usuario almacenaría el mismo objeto notificador, lo que no sería eficiente en relación al número de usuarios