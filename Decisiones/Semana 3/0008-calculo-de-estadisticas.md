# 0008 - Cálculo de estadísticas

- Status: accepted
- Date: 2026-11-17

## Context and Problem Statement

El sistema del periódico digital debe calcular cuatro estadísticas: noticias más leídas, tiempo de permanencia, tasa de rebote y conversión de lectores a suscriptores.

Para ello, necesitamos decidir cómo realizar estos cálculos a partir de los datos recogidos sobre la actividad de los lectores, manteniendo separada la obtención de datos de su procesamiento estadístico.

## Decision Drivers

- RF-6: Módulo de estadísticas.
- RF-6.1: Cálculo de tasa de rebote.

## Considered Options

- Implementación propia en una única clase.
- Librería de estadísticas.

## Decision Outcome

Hemos elegido una **implementación propia en una única clase** porque las cuatro estadísticas que necesita nuestro periódico digital están claramente definidas y podemos calcularlas sin depender de una librería externa.

De esta manera, mantenemos el control sobre cómo se calculan las noticias más leídas, el tiempo de permanencia, la tasa de rebote y la conversión de lectores a suscriptores.

Además, la clase de estadísticas se encargará únicamente de realizar los cálculos a partir de los datos disponibles, manteniendo separada la responsabilidad de recoger y preparar la información de los lectores.

### Consequences

- Good, because podemos calcular las cuatro estadísticas del periódico sin depender de librerías externas.
- Good, because mantenemos el control sobre cómo se calcula cada métrica, especialmente la tasa de rebote definida en el RF-6.1.
- Good, because separamos el cálculo de estadísticas de la recogida de datos, evitando mezclar ambas responsabilidades.
- Bad, because debemos desarrollar y mantener los cálculos de las cuatro estadísticas.
- Bad, because si en el futuro añadimos muchas estadísticas o cálculos más complejos, podría ser necesario dividir la clase en varios componentes.
## Pros and Cons of the Options

### Implementación propia en una única clase

Consiste en utilizar una clase dentro del módulo de estadísticas que realice los cálculos de las cuatro métricas del periódico a partir de los datos previamente recogidos y preparados.

Cada estadística tendrá su propio método de cálculo, sin que esta clase tenga que encargarse de registrar las visitas o recopilar la actividad de los lectores.

- Good, because podemos calcular las cuatro estadísticas del RF-6 sin añadir dependencias externas al sistema.
- Good, because mantenemos el control sobre las reglas de cálculo de cada estadística, especialmente la definición de tasa de rebote del RF-6.1.
- Good, because agrupamos los cálculos de las estadísticas en un único componente, manteniéndolos separados de la recogida de datos de los lectores.
- Bad, because tenemos que desarrollar y mantener nosotros los cálculos de las estadísticas.
- Bad, because si el número de estadísticas aumenta considerablemente, la clase podría acumular demasiadas responsabilidades y necesitar una división.

### Librería de estadísticas

Consiste en utilizar una librería externa que proporcione funciones matemáticas y estadísticas para calcular las métricas del periódico.

Aunque la librería facilitaría algunas operaciones, seguiríamos necesitando obtener los datos de las visitas y aplicar las reglas específicas de nuestras estadísticas.

- Good, because proporciona funciones estadísticas ya desarrolladas, evitando tener que implementar determinadas operaciones matemáticas.
- Bad, because las cuatro estadísticas que necesitamos son concretas y no requieren necesariamente una librería especializada.
- Bad, because seguiríamos teniendo que implementar la lógica propia del periódico, como determinar qué visitas se consideran rebotes o qué lectores se han convertido en suscriptores.
- Bad, because introduce una dependencia externa que debemos mantener y que puede estar condicionada por el lenguaje de programación utilizado.
- Bad, because tendríamos que comprobar que los resultados de la librería se ajustan a las definiciones establecidas en nuestros requisitos.
