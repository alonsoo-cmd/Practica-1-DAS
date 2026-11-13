# 0005 - Suscripción a canales de noticias

- Status: rejected
- Date: 2026-11-12

Technical Story: El sistema debe permitir que un lector se suscriba a una categoría de noticias o a un redactor específico.

## Context and Problem Statement

De qué forma gestiona el servidor el alta de un lector a una categoría de noticias o a un redactor en específico.

## Decision Drivers

- RF-3: Suscripción a canales de noticias.

## Considered Options

- Publish-Subscribe
- Observer
- Gestor de suscripciones (una sola clase)

## Decision Outcome

Chosen option: "Gestor de suscripciones", because el requisito solo exige registrar el alta, y esta opción es la más sencilla de las consideradas, funcionando igualmente bien.

### Positive Consequences

- Solución muy simple: un único objeto de suscripción que se corresponde con un registro de la base de datos de suscriptores.
- No añade intermediarios ni estructuras que mantener en memoria, lo que encaja con un servidor REST sin estado.

### Negative Consequences

- Al guardar solo el módulo, es difícil obtener estadísticas (por ejemplo, el número de suscriptores de un redactor o de un canal), ya que habría que revisar objeto por objeto quién está suscrito a cada cosa.
- Todo módulo que necesite consultar algo sobre suscriptores necesita consultar la clase.

## Pros and Cons of the Options

### Publish-Subscribe

Hay un canal por categoría y un intermediario que los gestiona todos a la vez. El lector se da de alta en el canal, por lo que quien publica no sabe directamente quién lee las noticias: solo las envía al gestor.

- Good, because los redactores no conocen a los lectores y la suscripción se hace en el canal, lo que encaja con el alta anónima.
- Good, because para darse de baja es muy simple: solamente hay que quitar al lector del canal, sin afectar a quien publica.
- Bad, because añade un intermediario para únicamente 5 categorías fijas, una complejidad que puede ser innecesaria.
- Bad, because saber a qué categorías está suscrito un lector obliga a recorrer los canales uno a uno.

### Observer

Cada categoría tiene una lista de suscriptores y, al suscribirse, se añade al lector a esa lista.

- Good, because la estructura es sencilla y sin intermediarios: la propia categoría gestiona el alta.
- Bad, because cada categoría conoce y mantiene la lista completa de sus suscriptores, por lo que sabe quién es cada uno.
- Bad, because la lista de suscriptores habría que reconstruirla en cada petición, ya que vive en memoria y REST no tiene estado.

### Gestor de suscripciones

Una clase gestiona el alta creando un objeto que une lector y categoría.

- Good, because es muy simple: hay un objeto de suscripción que se corresponde con un registro de la base de datos de suscriptores.
- Bad, because solo guarda el módulo, por lo que es difícil obtener estadísticas (por ejemplo, el número de suscriptores de un redactor o de un canal), ya que habría que ir objeto por objeto revisando quién está suscrito a cada cosa.
- Bad, because todo módulo que necesite consultar algo sobre suscriptores necesita consultar la clase.