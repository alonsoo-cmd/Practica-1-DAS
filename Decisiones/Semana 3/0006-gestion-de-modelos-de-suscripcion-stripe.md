# 0006 - Gestión de modelos de suscripción con Stripe:

* Status: accepted
* Date: 2026-11-17

## Context and Problem Statement

Con el objeto de acceder al contenido, la web del periódico digital ofrece 3 modalidades de pago diferentes: Trimestral (Cada tres meses, 70€), Semestral (Cada seis meses, 130€) y Anual (Cada doce meses, 190€). Los periodos de pago son recurrentes según los periodos mencionados. Se empleará la pasarela de pago Stripe. Se determinará como enlazar el sistema con el componente externo Stripe.

## Decision Drivers

* RF-5: Pago por suscripción al periódico
* RF-5.1: Renovación automática
* RD-2: Pasarela de pago Stripe

## Considered Options

* Patrón Facade 

## Decision Outcome

Escogemos la opción Patrón Facade porque proporciona una interfaz unificada para acceder a las funciones de pagos con Stripe separándola del resto del sistema. Será el intermediario que se comunicará con el componente de Stripe correspondiente.

### Consequences

* Good, because separa las responsabilidades y contiene la lógica de pagos, ocultándola al resto del sistema.
* Good, because facilita el mantenimiento del sistema por centralizar la interacción con Stripe en una sola parte. Permite enlazar de forma más sencilla con otros componentes que requieran realizar un pago, y el modificar los detalles de la integración sin modificar el resto de partes del sistema (por ejemplo, reintentos).
* Bad, because puede sobrecargar la fachada si concentra demasiada lógica.

## Pros and Cons of the Options

### Patrón Facade

Se emplea una clase "Fachada" que implemente el patrón Facade, que se encarga de interactuar con Stripe para simplificar el acceso a las peticiones del componente Stripe correspondiente. Esta gestionará la lógica de pagos.

* Good, because separa las responsabilidades y contiene la lógica de pagos, ocultándola al resto del sistema.
* Good, because centraliza la interacción con Stripe en una sola parte. Esto permite enlazar de forma más sencilla con otros componentes que requieran realizar un pago, y poder modificar los detalles de la integración sin modificar otras partes del sistema (por ejemplo, reintentos).
* Bad, because puede sobrecargar la fachada si concentra demasiada lógica.

## More information

https://docs.stripe.com/
