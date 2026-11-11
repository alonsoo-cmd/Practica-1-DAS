# 0001 - Selección de Estilo Arquitectónico Principal

*Decisión modificada como consecuencia de una mala comunicación y la inclusión como alternativa de un estilo que no encaja con nuestra arquitectura*

- Status: accepted
- Date: 2026-11-07

Technical Story: Definición del estilo de arquitectura de software para el sistema de periódico digital con suscripción.

## Context and Problem Statement

Se necesita definir el estilo arquitectónico principal para soportar un periódico digital responsivo, con comunicación REST entre cliente y backend y persistencia distribuida en dos bases de datos PostgreSQL 19 aisladas.

## Decision Drivers

- RF-1: Discriminación de dispositivos (adaptación de interfaz cliente PC/Tablet mediante HTTP/REST).
- RD-1: Comunicación HTTP/REST (comunicación mediante API REST entre frontend y backend).
- RD-3: Persistencia en PostgreSQL 19 (dos bases de datos independientes, una para redactores/administradores y otra para suscriptores).

## Considered Options

- Cliente-Servidor en 3 Capas (Tiers)
- Arquitectura de Microservicios

## Decision Outcome

Chosen option: "Cliente-Servidor en 3 Capas", because es la opción que mejor se adapta a los Requisitos de Dominio elegidos, canalizando las peticiones HTTP/REST a través de una capa intermedia de lógica de negocio y separando adecuadamente la presentación del acceso a las dos bases de datos PostgreSQL 19.

### Positive Consequences

- Clara separación de responsabilidades entre Presentación, Lógica y Datos.
- Oculta las dos bases de datos PostgreSQL 19 al cliente web por motivos de seguridad.
- Permite implementar las peticiones HTTP/REST de forma fácil
- El cliente nunca accede directamente a los datos.

### Negative Consequences

- La capa de lógica de negocio es compacta, por lo que si sufre un fallo severo puede afectar al bloque entero.
- Las métricas que combinan datos de ambas bases de datos independientes añaden complejidad al requerir agregación en el servidor de aplicación.

## Pros and Cons of the Options

### Cliente-Servidor en 3 Capas

Una arquitectura cliente-servidor en la que un cliente web responsivo se comunica con un backend a través de una API REST y persiste los datos en dos bases de datos SQL independientes. Separa las responsabilidades en presentación, lógica de negocio y acceso a datos.

- Good, because se separan responsabilidades: el cliente se encarga únicamente de mostrar la interfaz responsiva mientras el servidor contiene la lógica y la persistencia.
- Good, because podemos implementar las peticiones HTTP/REST sin problemas.
- Good, because el cliente no accede nunca directamente a las bases de datos, mejorando la seguridad.
- Bad, because la lógica se despliega en el mismo servicio de aplicación, aumentando la latencia frente a 2 capas.

### Arquitectura de Microservicios

Se usa un servicio independiente por cada sección del negocio con una responsabilidad distinta cada uno.

- Good, because cada servicio se escala de forma independiente aislando fallos y protegiendo los servicios críticos.
- Bad, because añade una complejidad inecesaria al tener que gestionar 2 bases de datos distintas.
- Bad, because introduce una gran complejidad operativa y de gobierno de datos, desproporcionada para la escala del sistema.

