# 0004 - Discriminación de clientes

- Status: accepted
- Date: 2026-11-12

## Context and Problem Statement

El sistema del periódico digital debe distinguir si el lector accede desde un PC o una tablet para proporcionarle el contenido adaptado a su dispositivo.

Para ello, necesitamos decidir cómo identificar el tipo de cliente sin que los distintos módulos del periódico tengan que encargarse de esta responsabilidad.

## Decision Drivers

- RF-2: Discriminación de clientes.

## Considered Options

- Intercepting Filter.
- API Gateway.

## Decision Outcome

Hemos elegido **Intercepting Filter** porque permite identificar el tipo de cliente en un punto común, antes de que la petición llegue a los módulos del servidor.

De esta manera, la identificación queda separada de la lógica de negocio del periódico, sin necesidad de añadir un componente como API Gateway, que consideramos demasiado complejo para nuestra arquitectura con un único backend.

### Consequences

- Good, because los módulos de noticias, suscripciones y pagos no tienen que encargarse de identificar si el lector utiliza un PC o una tablet.
- Good, because la identificación se realiza en un único punto, manteniendo esta responsabilidad separada del resto de funcionalidades del periódico.
- Good, because si en el futuro necesitamos reconocer otros dispositivos, podemos ampliar el filtro sin modificar los módulos del periódico.
- Bad, because añadimos un filtro al procesamiento de las peticiones, aunque únicamente necesitamos distinguir dos tipos de dispositivos.
- Bad, because debemos decidir cómo tratar las peticiones que no se puedan identificar como PC o como tablet.

## Pros and Cons of the Options

### Intercepting Filter

Consiste en colocar un filtro antes de los controladores del servidor que identifique si la petición procede de un PC o una tablet, antes de que llegue a los módulos del periódico.

- Good, because centraliza la identificación de los dispositivos, evitando que los módulos de noticias, suscripciones o pagos tengan que realizarla por separado.
- Good, because encaja con nuestra arquitectura HTTP/REST, ya que podemos identificar el tipo de cliente al recibir sus peticiones.
- Bad, because introduce un mecanismo adicional para una funcionalidad que actualmente solo necesita distinguir entre PC y tablet.
- Bad, because debemos contemplar qué ocurre cuando un lector accede desde un dispositivo que el filtro no reconoce.

### API Gateway

Consiste en introducir un componente entre el cliente web y el servidor del periódico, encargado de recibir las peticiones e identificar el tipo de dispositivo antes de enviarlas al backend.

- Good, because permite identificar si el lector utiliza un PC o una tablet antes de que la petición llegue al servidor del periódico.
- Good, because mantiene la identificación de dispositivos fuera del backend, evitando que los módulos de noticias, suscripciones y pagos tengan que encargarse de ella.
- Bad, because nuestro periódico utiliza un único backend, por lo que añadir un API Gateway únicamente para distinguir dos dispositivos supone una complejidad innecesaria.
- Bad, because introduce un componente adicional que debemos mantener, cuando podemos realizar la identificación directamente mediante un filtro.
