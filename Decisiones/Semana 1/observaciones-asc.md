
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

Pendiente de incorporar.

### Respuesta de los ASS

Pendiente de discutir con Alonso e Izan.

### Conclusión

Pendiente de acordar.

---

## MADR 0002 - Gestión de notificaciones y suscripciones

### Observaciones ASC

Pendiente.

### Respuesta de los ASS

Pendiente.

### Conclusión

Pendiente.

---

## MADR 0003 - Gestión de pagos con Stripe

### Observaciones ASC

Pendiente.

### Respuesta de los ASS

Pendiente.

### Conclusión

Pendiente.
