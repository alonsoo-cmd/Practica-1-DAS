# Selección-Estilo-Arquitectónico

* Status: proposed
* Date: 2026-11-07

Technical Story: Estilo de arquitectura de software de periodico digital con suscripción

## Context and Problem Statement

Se necesita definir estilo arquitectonico principal de un periodico digital en el que los suscriptores puedan suscribirse a noticias por categorías. ¿Que estilo arquitectonico debe usarse en los distintos subsistemas y servir de base a las posteriores decisiones de diseño?

## Decision Drivers

* RD-01
* RD-05
* RD-03

## Considered Options

* Cliente-Servidor
* Microservicios
* MVC

## Decision Outcome

Chosen option: "Cliente-Servidor", because Es la que mejor se adapta a los tres RD que hemos elegido, separando claramente las responsabilidades

### Positive Consequences

* Separación de responsabilidades
* Se puede ampliar mediante una caché para picos de lectura
* El cliente nunca accede directamente a los datos

### Negative Consequences

* La capa de lógica es compacta, por lo que si algo falla puede afectar al bloque entero
* No queda claro de que forma se van a implementar las notificaciones a suscriptores

## Pros and Cons of the Options

### Cliente-Servidor

Una arquitectura cliente-servidor en la que un cliente web se comunica con un back-end a traves de una API REST y que persiste los datos en dos bases de datos SQL independientes. 
Separa las responsabilidades en presentación, lógica de negocio y acceso a datos

* Good, because Se separan responsabilidades, el cliente se encarga unicamente de mostrar la interfaz a los usuarios, mientras el servidor se encarga de contener la lógica y de la persistencia
* Good, because El cliente no accede nunca directamente a las bases de datos, mejorando la seguridad
* Good, because Podemos apoyarnos y complementar la arquitectura con una cache propia de REST para que la aplicación resista en picos de lectura
* Bad, because La lógica se desplega en el mismo servicio, por lo que si algo falla puede afectar al resto de la aplicación
* Bad, because Las métricas que combinan datos de ambas bases de datos añaden complejidad ya que la capa lógica tiene que acceder a las dos bases de datos a la vez

### Microservicios

Se usa un servicio independiente por cada sección del negocio con una responsabilidad distinta cada uno

* Good, because Cada servicio se escala de forma independiente aislando fallos y protegiendo la mayor parte de nuestra aplicación
* Bad, because Contradice el patrón de base de datos ya que tendremos dos distintas
* Bad, because Se introduce una gran complejidad, desproporcionada para el tamaño del sistema

### MVC (Modelo-Vista-Controlador)

Permite separar las responsabilidades de la aplicación web en tres partes (Modelo: Acceso a base de datos y lógica de negocio de operaciones de suscripción y usuarios | Vista: Front-end de la web con HTML | Controlador: Maneja comunicación con API y microservicios)

* Good because separa claramente las necesidades de las diferentes partes de la aplicación entre las dos bases de datos y la logica de negocio, el frontend y la interfaz del cliente gestionada mediante vistas, además de un controlador que maneja la comunicación entre estas dos partes.
* Good because permite ampliar de forma sencilla cada una de los módulos de forma individual, en caso de que se quiera hacer una amplicación en el futuro de la aplicación
* Bad because la separación podría introducir complejidad innecesaria en la aplicación por no ser excesivamente compleja
* Bad, because Las métricas que combinan datos de ambas bases de datos añaden complejidad ya que la capa lógica tiene que acceder a las dos bases de datos a la vez
