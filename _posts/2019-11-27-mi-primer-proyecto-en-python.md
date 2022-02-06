---
layout: post
title: "Mi primer proyecto en Python"
tags: [articulo]
---

Decidí aprender a programar en Python por curiosidad hace un año atrás. Hay muchísima información gratuita en Internet para aprender los conceptos básicos de la sintaxis y los campos de aplicación. Tras algunas semanas, logré automatizar varias tareas de la oficina en la que trabajo, y abandoné Python hasta el domingo pasado.

[EpubLibre](http://epublibre.org) está trabajando en la versión en formato .epub del Borges de Bioy Casares: un libro que quiero leer y que, en MercadoLibre, se puede adquirir por un valor que ronda los $12.000. Demasiado.

Entonces, se me ocurrió la siguiente idea para un proyecto en Python: automatizar un seguimiento de cada e-book publicado en EpubLibre y almacenar los resultados en una base de datos. Para hacerlo más interesante, que cada vez que esto suceda (que un nuevo libro se suba a la web de EpubLibre) automáticamente se genere un tuit en mi cuenta de Twitter, para que mis seguidores ahí también reciban la novedad.

(Aclaración necesaria: no soy un programador. Es posible que mi código pueda ser escrito con mucha más simpleza o profesionalismo. Como apenas soy un tipo curioso, mi pretensión es sencillamente que funcione).

La dinámica del script consiste en:

1. Capturar la sección *Novedades* de la web de EpubLibre.
2. Listar los ebooks observables (un catálogo permanente de 18 ebooks que van actualizándose de modo tal que al subir uno nuevo, el último en orden cronológico deja de ser visible en la sección).
3. Comparar esa lista de ebooks con el de una base de datos preexistente.
4. Si hay un ebook nuevo, anexarlo a la base de datos.
5. Publicar un tuit que informe la existencia del nuevo ebook.
6. Repetir periódicamente y de forma automática.

El código lo encuentran en [este repositorio](https://github.com/catorceveces/ebookscraper) de GitHub.

**UPDATE:** Funciona. Así que, ya saben. Si quieren enterarse de qué libros se pubican en EpubLibre, síganme en [twitter](http://www.twitter.com/catorceveces).
