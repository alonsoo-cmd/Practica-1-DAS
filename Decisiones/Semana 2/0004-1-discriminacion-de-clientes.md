# 0004 - Discriminación de clientes

- Status: accepted
- Date: 2026-11-12

Technical Story: El sistema debe distinguir qué tipo de dispositivo usa el cliente, que puede ser PC o tablet.

## Context and Problem Statement

Se necesita que el sistema distinga qué tipo de dispositivo está usando el cliente para decidir qué tipo de frontend y qué tipo de contenido debe proporcionarle.

## Decision Drivers

- RF-2: Discriminación de clientes.

## Considered Options

- Clase identificadora
- Chain of Responsibility
- Intercepting Filter (Fuente: [Oracle](https://www.oracle.com/java/technologies/intercepting-filter.html) y [Baeldung](https://www.baeldung.com/intercepting-filter-pattern-in-java))

## Decision Outcome

Chosen option: "Intercepting Filter", because se adapta completamente a la filosofía REST, realizando la comprobación en cada petición en un único punto de paso.

### Positive Consequences

- La petición se analiza una sola vez en un único punto, sin romper la modularidad como ocurriría con la clase identificadora.
- Encaja con REST sin estado, ya que cada petición pasa por el filtro.
- La petición llega ya clasificada a los módulos, porque el filtro le asigna un tipo antes de que llegue a ninguno de ellos.

### Negative Consequences

- Añade más clases que la clase identificadora (gestor, cadena, interfaz de filtro y filtro concreto).
- Es necesario añadir alguna forma de categorizar las peticiones que no encajan entre las consideradas posibles, como las que no son ni de tablet ni de PC.

## Pros and Cons of the Options

### Clase identificadora

Una única clase que recibe una petición y distingue de qué dispositivo viene. Tiene un método para distinguir la petición y un enumerado.

- Good, because es una solución extremadamente simple: solamente una clase y un enumerado.
- Good, because solo se identifican las peticiones necesarias en los momentos necesarios, no hay por qué analizarlas todas.
- Bad, because delega en cada parte de la lógica del periódico la identificación de la petición. Por ejemplo, si una petición viene de la parte de suscripciones, será el propio módulo de suscripciones quien se la dé a la clase, aumentando el acoplamiento y provocando una modularidad más baja.
- Bad, because si una petición pasa por dos módulos se podría identificar dos veces.

### Chain of Responsibility

La petición recorre una cadena y cada manejador comprueba si el cliente es el suyo; si no lo es, pasa al siguiente.

- Good, because la responsabilidad de reconocer a cada cliente queda en el propio manejador.
- Good, because si se quiere añadir un nuevo tipo, únicamente hay que añadir un nuevo manejador.
- Bad, because una petición que no se reconoce y no tiene manejador llegaría al final de la cadena sin que ningún manejador la reconozca, por lo que se queda sin tipo.
- Bad, because montar manejadores encadenados para solo dos tipos es desproporcionado y aporta más complejidad de la necesaria al código.

### Intercepting Filter

Un filtro colocado delante de todos los controladores que examina la petición y le asigna un tipo antes de que llegue a ningún módulo.

- Good, because la petición se analiza solo una vez en un solo punto, pero sin romper la modularidad como en la clase identificadora.
- Good, because encaja con REST sin estado, ya que cada petición pasa por el filtro.
- Bad, because añade más clases que la clase identificadora (gestor, cadena, interfaz de filtro y filtro concreto).