# 0009 - Suscripción a canales de noticias

- Status: accepted
- Date: 2026-11-17

Technical Story: El sistema debe permitir que un lector se suscriba a una o varias categorías de noticias de forma anónima.

## Context and Problem Statement

El sistema del periódico digital debe permitir que un lector se suscriba a una o varias de las 5 categorías de noticias: política, economía, sociedad, nacionales e internacionales.

Para ello, necesitamos decidir cómo gestiona el backend el alta de un lector en una categoría y cómo se representan las categorías.

## Decision Drivers

- RF-3: Suscripción a canales de noticias.
- RF-4: Clasificación de noticias.

## Considered Options

- Gestor de suscripciones con jerarquía de herencia de Categoría.
- Gestor de suscripciones con varios tipos de categorías.

## Decision Outcome

Hemos elegido un **gestor de suscripciones con varios tipos de categorías** porque es la forma más simple de representar las categorías y concreta un único punto que gestiona el alta de los lectores.

### Consequences

- Good, because facilita la gestión del anonimato, ya que el alta del lector se hace mediante un registro anónimo.
- Good, because es fácil de implementar y no añade complejidad.
- Bad, because si queremos añadir una categoría debemos modificar la clase.

## Pros and Cons of the Options

### Gestor de suscripciones con jerarquía de herencia de Categoría

Consiste en un gestor que guarda las suscripciones, donde cada categoría es una subclase de una clase abstracta Categoría.

- Good, because podríamos diferenciar el comportamiento de cada categoría.
- Bad, because no necesitamos tener una clase por cada categoría, ya que no se comportan de forma distinta.
- Bad, because una noticia solo puede pertenecer a una sola categoría.

### Gestor de suscripciones con varios tipos de categorías

Consiste en un gestor que guarda los suscriptores y una única clase que contiene todos los tipos de categorías de noticias.

- Good, because es una representación simple de un conjunto fijo de valores.
- Good, because las categorías se definen en un único punto, por lo que son fijas y no hay ambigüedad.
- Bad, because no se pueden crear nuevas categorías sin modificar la clase.
