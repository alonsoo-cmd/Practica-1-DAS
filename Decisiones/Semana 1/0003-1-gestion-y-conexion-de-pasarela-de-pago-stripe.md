

# Gestión de pagos, modelos de suscripción, y reintentos integrando Stripe

## Context and Problem Statement

La aplicación web del periódico digital, aunque deja ver contenido gratuitamente, también ofrece una suscripción de pago para acceder a ciertas funciones. Este pago puede ser reintentado hasta 3 veces lo cual produce un bloqueo de 24h, y 3 modalidades que ofrecen varios tipos de descuento.

## Decision Drivers

* RF-2: Modalidades de pago
* RF-2.1: Renovación automática
* RF-2.2: Gestión de pagos fallidos
* RF-2.3: Gestión de renovaciones fallidas
* RD-4: Pasarela de pago STRIPE

## Considered Options

* Implementación con SDK
* Implementación con API Stripe
* Implementación con SDK + Stripe Billing
* Implementación con API Stripe + Stripe Billing

## Decision Outcome

Chosen option: "Implementación con SDK + Stripe Billing", because la opción elegida proporciona un equilibrio entre flexibilidad, prestaciones, facilidad de implementación y precio.


### Consequences

* Good, because facilita la implementación y mantenimiento al no tener que implementar directamente las peticiones con API REST, manejo de errores y gran parte de la lógica.
* Good, because Stripe Billing maneja directamente la creación de planes de suscripción, renovación automática y los reintentos de pago. Mayor facilidad de introducir cambios sin tocar el código.
* Bad, because la implementación presenta una menor flexibilidad que al trabajar directamente con la API.
* Bad, because "Stripe Billing" requiere una suscripción de pago.


## Pros and Cons of the Options

### Implementación con SDK

* Good, because facilita la implementación y mantenimiento al no tener que implementar directamente las peticiones con API REST, manejo de errores y gran parte de la lógica.
* Bad, because la implementación presenta una menor flexibilidad que al trabajar directamente con la API.
* Bad, because la implementación de los reintentos, suscripciones, y planes de pago deben ser desarrollados manualmente. Más posibilidades de bugs y aumenta coste de mantenimiento.

### Implementación con API Stripe

* Good, because es mucho más flexible a modificaciones y personalización, al ser gestionado directamente mediante el código escrito.
* Bad, because la implementación de los reintentos, suscripciones, y planes de pago deben ser desarrollados manualmente. Más posibilidades de bugs y aumenta coste de mantenimiento.

### Implementación con API Stripe + Stripe Billing

* Good, because Stripe Billing maneja directamente la creación de planes de suscripción, renovación automática y los reintentos de pago. Mayor facilidad de introducir cambios sin tocar el código.
* Bad, because "Stripe Billing" requiere una suscripción de pago.