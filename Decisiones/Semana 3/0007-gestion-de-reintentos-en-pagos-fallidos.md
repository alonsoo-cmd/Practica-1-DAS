# 0007 - Gestión de reintentos en pagos fallidos

* Status: accepted
* Date: 2026-11-17

## Context and Problem Statement

El sistema del periódico digital utiliza Stripe para gestionar los pagos de las suscripciones.

Según el RF-5.2, cuando un pago falla, el lector puede volver a intentarlo manualmente hasta tres veces más, es decir, un máximo de cuatro intentos en total.

Para ello, necesitamos decidir cómo gestionar estos reintentos y controlar que no se supere el número permitido.

## Decision Drivers

* RF-5.2: Gestión de pagos fallidos.
* RD-2: Pasarela de pago Stripe.

## Considered Options

* Patrón Retry.
* Librería Tenacity.

## Decision Outcome

Hemos elegido Patrón Retry porque permite gestionar los reintentos de manera independiente a la lógica de pagos del periódico.

En nuestro caso, adaptaremos el patrón para que sea el lector quien decida cuándo volver a intentar el pago, mientras que el mecanismo Retry controlará que no se superen los tres intentos adicionales permitidos.

Además, esta solución nos permite gestionar los reintentos sin depender de una librería externa ni de un lenguaje de programación concreto, como ocurriría con Tenacity.

### Consequences

* Good, because los reintentos se gestionan de forma independiente al procesamiento de los pagos mediante Stripe.
* Good, because permite controlar que cada lector disponga únicamente de tres intentos adicionales cuando falla un pago.
* Good, because podemos modificar las condiciones de los reintentos sin tener que cambiar la lógica de pagos del periódico.
* Bad, because debemos desarrollar nuestro propio mecanismo para controlar los reintentos.
* Bad, because necesitamos guardar el número de intentos realizados para evitar que el lector pueda superar el límite permitido.

## Pros and Cons of the Options

### Patrón Retry

Consiste en utilizar un mecanismo Retry que controle los reintentos de pago realizados por el lector. Cuando falla un pago mediante Stripe, el sistema comprueba cuántos intentos se han realizado y permite volver a intentarlo manualmente mientras no se supere el límite establecido.

* Good, because permite adaptar el mecanismo de reintentos para que sea el lector quien decida cuándo volver a intentar el pago.
* Good, because no requiere utilizar librerías externas ni depender de un lenguaje de programación concreto.
* Bad, because requiere desarrollar, probar y mantener un mecanismo de control de reintentos propio.


### Librería Tenacity

Consiste en utilizar Tenacity, una librería de Python especializada en gestionar reintentos de operaciones fallidas. Permite configurar el número máximo de intentos y las condiciones en las que se repite una operación.

Para utilizarla en nuestro periódico, tendríamos que adaptar su funcionamiento para que los reintentos dependan de la decisión del lector.

* Good, because proporciona un mecanismo de reintentos ya desarrollado y configurable, reduciendo el trabajo de implementación.
* Bad, because está desarrollada para Python, por lo que condiciona la tecnología utilizada en nuestro backend.
Bad, because Tenacity está pensada principalmente para realizar reintentos automáticos, mientras que en nuestro periódico es el lector quien decide cuándo volver a intentar el pago. 
* Bad, because introduce una dependencia externa para gestionar únicamente tres reintentos adicionales.
