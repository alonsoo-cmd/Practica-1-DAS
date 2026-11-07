# Observaciones ASC - Semana 1

En este documento recogemos las observaciones de los arquitectos cognitivos sobre las decisiones planteadas por los ASS durante la primera semana.

La idea es revisar los MADR, comentar los puntos que creemos que se pueden mejorar y llegar a un acuerdo antes de modificar las decisiones originales.

## MADR 0001 - Selección del estilo arquitectónico

### Observaciones de Jorge

**1. Identificadores de los requisitos**

En los Decision Drivers están intercambiados los identificadores RD-3 y RD-5.

- RD-3: Comunicación HTTP/REST.
- RD-5: Persistencia en PostgreSQL 19.

Habría que corregirlos para que coincidan con la tabla de requisitos.

**2. Comparación entre cliente-servidor y MVC**

Creo que MVC no debería plantearse como una alternativa excluyente a cliente-servidor, ya que podríamos utilizar ambos conjuntamente.

Cliente-servidor define la comunicación entre los clientes y el servidor, mientras que MVC permite organizar las responsabilidades internas de la aplicación.

Por tanto, propongo mantener cliente-servidor como posible estilo general y valorar MVC por separado, si necesitamos decidir cómo organizar internamente el servidor.

**3. Microservicios y bases de datos**

En los inconvenientes de microservicios se indica que esta arquitectura contradice el uso de dos bases de datos.

No estoy de acuerdo con ese argumento, porque los microservicios pueden gestionar sus propios datos de forma independiente.

Creo que sería más adecuado señalar la complejidad adicional de comunicación y coordinación entre servicios, especialmente cuando necesitamos combinar información de noticias y suscripciones para calcular estadísticas.

**4. Seguridad y acceso a las bases de datos**

Se menciona como ventaja de cliente-servidor que el cliente no accede directamente a las bases de datos.

Aunque es una ventaja, no es exclusiva de este estilo. En microservicios también podemos controlar el acceso a los datos a través de los propios servicios.

Mantendría este punto como consecuencia positiva, pero no como argumento para descartar microservicios.

**5. Uso de caché**

También revisaría el argumento de la caché para los picos de lectura, porque no es algo exclusivo de cliente-servidor.

Podemos mantenerlo como una posible mejora de la arquitectura elegida, pero no creo que deba utilizarse como una ventaja frente a las demás alternativas.

### Valoración general

Por mi parte, considero razonable elegir cliente-servidor como arquitectura general del periódico, principalmente por la sencillez de la solución y porque permite separar el front-end de la lógica del servidor y del acceso a los datos.

Mis observaciones van dirigidas sobre todo a mejorar la justificación de la decisión y la comparación de alternativas, no necesariamente a cambiar la opción elegida.

### Observaciones de Víctor

**1. Evaluación de alternativas de diseño (Regla del 75%)**
Revisar que en el documento MADR se incluyan explícitamente al menos dos alternativas reales de arquitectura (como Cliente-Servidor vs. Microservicios) bien comparadas, para cumplir con el requisito de la asignatura de evaluar más de una opción.

**2. Justificación de la solución escogida**
Apoyo la decisión de utilizar la arquitectura Cliente-Servidor en 3 Capas. La justificación principal en la decisión debe centrarse en que es la opción más sencilla de desarrollar y desplegar, permitiendo separar la interfaz web responsiva (PC/Tablet) de la lógica del servidor y de las dos bases de datos PostgreSQL 19 independientes.

### Respuesta de los ASS

Pendiente de discutir con Alonso e Izan.

### Conclusión

Pendiente de acordar.

---

## MADR 0002 - Gestión de notificaciones y suscripciones

### Observaciones ASC

**1. Definición del patrón de notificaciones**
Debemos evitar definir esta decisión como un patrón de diseño a nivel de código interno (como Observer o Decorator) y enfocarlo hacia la arquitectura necesaria para distribuir las noticias.

**2. Anonimato en las suscripciones RSS**
El requisito aclara que la suscripción a los canales de noticias RSS debe ser anónima (sin datos personales). Se propone evaluar el patrón **Publicador-Suscriptor (Publish-Subscribe)** frente a realizar consultas periódicas (Polling HTTP), ya que permite notificar novedades por categorías sin requerir registro de los lectores.

### Respuesta de los ASS

Pendiente.

### Conclusión

Pendiente.

---

## MADR 0003 - Gestión de pagos con Stripe

### Observaciones ASC

**1. Trazabilidad con la tabla de requisitos**
Asegurar que esta decisión utiliza como Decision Driver principal la pasarela Stripe (RD-4) y que las modalidades de suscripción (70€, 130€ y 190€) junto a la regla de los 3 intentos de pago fallidos quedan asociadas correctamente a sus códigos de requisitos.

**2. Manejo de fallos en el cobro**
Conviene dejar definido en el diseño cómo reacciona el sistema cuando falla la conexión con Stripe para garantizar la suspensión temporal de 24 horas tras los 3 intentos.

### Respuesta de los ASS

Pendiente.

### Conclusión

Pendiente.
