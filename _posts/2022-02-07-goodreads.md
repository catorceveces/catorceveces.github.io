---
layout: post
title: "Goodreads"
tags: [proyectos]
description: "Un análisis sobre hábitos de consumo y tendencias considerando los primeros 10 mil libros de la lista Best Books Ever de Goodreads"
---

Con más de 125 millones de miembros (al 29/11/2021), Goodreads es la comunidad de lectores más importante de Internet. Su base de datos cuenta con 3.5 billones de libros indexados y 80 millones de reviews. Si existe un lugar del que recolectar información para establecer y analizar hábitos de lectura o consumos relacionados a los libros, Goodreads parece ser ese lugar.

La app permite, entre otras cosas, generar listas de libros según varios criterios (los mejores de libros de un género en particular, los libros mejor valorados de un siglo específico, los 1001 libros que hay que leer antes de morir, etc.). Hay, entre esas listas, una en la que más usuarios han participado: __Best books ever__, cuya descripción detalla: *The best books ever, as voted on by the general Goodreads community*.

En este proyecto se trabajará con un dataset compuesto por los primeros diez mil libros de esta lista (obtenidos al 30/05/2021). De cada uno de estos diez mil libros será extraída la siguiente información: título, autor, cantidad de páginas, año de publicación, rating, avr rating.

---

Una de las primeras preguntas que podemos hacernos tiene que ver con la fecha de publicación de los libros que componen nuestro dataset. Desde la teoría literaria se ha debatido acaloradamente en torno a la relación entre mercado y academia. Los mecanismos a través de los cuales se juzgan las virtudes de un libros son distintos, como también la adquisición del estatus de ‘clásico’ y el prestigio que ello supone. Con el prestigio, el libro adquiere difusión, aumenta su capital simbólico y, por consiguiente, su número de lectores.

Tendremos en cuenta los libros que hayan sido publicados con posterioridad al año 1500. Debido a que la creación de la imprenta de Gutenberg (1440) inició el proceso de difusión de libros y la posibilidad de adquirirlos por un número cada vez mayor de personas.

Una distribución inicial por siglo de los libros indexados en nuestro dataset genera el siguiente gráfico:

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/001_books_since_1500.png" | relative_url }}">
</p>

Observamos un llamativo salto exponencial de libros indexados cuya fecha de publicación resulta posterior al año 2000. Esto por sí solo debería resultar indicador suficiente de que los criterios académicos de valoración literaria no son relevantes para los usuarios de Goodreads. Basta con observar el plan de estudios de cualquier universidad para carreras humanísticas para descubrir que allí no abunda bibliografía editada en este siglo.

En una visualización con un criterio temporal más acotado:

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/001_books_since_1900.png" | relative_url }}">
</p>
<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/001_books_since_1980.png" | relative_url }}">
</p>
---

Al momento de filtrar los datos para localizar el período en que más libros han sido indexados en la lista por año de publicación, descubrimos que hay sólo tres años que cuentan con más 500 libros: 523 (en 2011), 555 (en 2012), 526 (en 2013).  Si efectuamos nuevamente el filtro para valores de más de 400 libros, el resultado suma los dos años previos: 407 (en 2009) y 425 (en 2010).

Comparemos esta información con la cantidad de libros indexados que se publicaron en 1967 (primera edición de *Cien años de soledad* de Gabriel García Márquez y momento de auge del boom latinoamericano): apenas 27. O con el promedio de libros publicados por año durante el siglo XX: 32.16.

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/002_books_b_2001_2015.png" | relative_url }}">
</p>

La diferencia es sustancial. ¿Es posible, además, que resulte indicativa de un tipo peculiar de consumo en la medida en que estos libros comparten ciertas temáticas?

Puesto que hemos relevado las etiquetas con las que han sido catalogados cada uno de los libros de nuestro dataset, podemos analizarlas en busca de tags compartidas que evidencien temáticas en común. Para ello, nos limitaremos al subconjunto de libros publicados entre 2009 hasta 2013. Es decir, el período álgido de la curva exponencial.

Este subconjunto, entonces, está compuesto de 2436 libros y en total suman 32.155 etiquetas. ¿Cuáles son las más empleadas y, por tanto, las compartidas por la mayor cantidad de libros?

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/003_tags.png" | relative_url }}">
</p>

Las veinticinco etiquetas con más ocurrencias nos brindan un panorama de qué tipo de ficción se está consumiendo: fantasía, romance, paranormal, aventura, adultos, fantasía urbana, romance paranormal (?).

*(Aclaración: algunos libros poseen dos veces la misma etiqueta; lo que, lejos de entorpecer el muestreo, lo vuelve aún más valioso, en la medida en que se refuerza cierto elemento en particular).*

Gran parte de este tipo de ficción es de reciente data en lo que hace a su género. Tomemos como referencia la ciencia ficción (uno de los géneros fundamentales de la segunda mitad del siglo XX), en comparación con otras etiquetas.

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/004_chicklit_sfiction.png" | relative_url }}">
</p>
<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/004_ufantasy_sfiction.png" | relative_url }}">
</p>
<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/004_promance_sfiction.png" | relative_url }}">
</p>

No existen libros indexados que posean la etiqueta paranormal-romance, por ejemplo, previos al año 1990. Generemos una tabla con los tres libros más antiguos de cada etiqueta de nuestro subconjunto para el dataset general. Prácticamente podemos rastrear el momento histórico en que cierto tipo de literatura empieza a ser producida.

<table style="width:100%">
  <thead>
    <tr style="text-align: right;">
      <th>Title</th>
      <th>Author</th>
      <th>Year</th>
      <th>Genre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Utopia</td>
      <td>Thomas More</td>
      <td>1516</td>
      <td>science-fiction</td>
    </tr>
    <tr>
      <td>Frankenstein: The 1818 Text</td>
      <td>Mary Wollstonecraft Shelley</td>
      <td>1818</td>
      <td>science-fiction</td>
    </tr>
    <tr>
      <td>Phantastes</td>
      <td>George MacDonald</td>
      <td>1858</td>
      <td>science-fiction</td>
    </tr>
    <tr>
      <td>Miss Pettigrew Lives for a Day</td>
      <td>Winifred Watson</td>
      <td>1938</td>
      <td>chick-lit</td>
    </tr>
    <tr>
      <td>Forever Amber</td>
      <td>Kathleen Winsor</td>
      <td>1944</td>
      <td>chick-lit</td>
    </tr>
    <tr>
      <td>Valley of the Dolls</td>
      <td>Jacqueline Susann</td>
      <td>1966</td>
      <td>chick-lit</td>
    </tr>
    <tr>
      <td>Interview with the Vampire</td>
      <td>Anne Rice</td>
      <td>1976</td>
      <td>urban-fantasy</td>
    </tr>
    <tr>
      <td>Fevre Dream</td>
      <td>George R.R. Martin</td>
      <td>1982</td>
      <td>urban-fantasy</td>
    </tr>
    <tr>
      <td>The Armageddon Rag</td>
      <td>George R.R. Martin</td>
      <td>1983</td>
      <td>urban-fantasy</td>
    </tr>
    <tr>
      <td>The Silver Kiss</td>
      <td>Annette Curtis Klause</td>
      <td>1990</td>
      <td>paranormal-romance</td>
    </tr>
    <tr>
      <td>The Fury / Dark Reunion</td>
      <td>L.J. Smith</td>
      <td>1991</td>
      <td>paranormal-romance</td>
    </tr>
    <tr>
      <td>The Awakening / The Struggle</td>
      <td>L.J. Smith</td>
      <td>1991</td>
      <td>paranormal-romance</td>
    </tr>
  </tbody>
</table>

---

Algo más sobre formatos: una comparación entre la progresión a través del tiempo de las etiquetas ‘novels’ y ‘poetry’.

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/005_novels_poetry.png" | relative_url }}">
</p>

---

Detengamonos un momento en dos etiquetas en particular: __chick-lit__ y __womens-fiction__. Que estas tags se encuentren entre las veinticinco más empleadas en el momento de mayor indexación de libros que conforman nuestro dataset permite adoptar una postura optimista en lo que respecta al acompañamiento que, desde el ámbito de la literatura, se hace de movimientos de reivindicación que están anclados estrictamente en lo político.

En lo que respecta a la incorporación de mujeres al mundo de la literatura, un mundo que históricamente ha sido restrictivo de los hombres — y que, a su vez, ha pautado comportamientos sociales (Madame Bovary es, tal vez, el mejor ejemplo). Y asimismo en lo que concierne a las formas en la que fueron reconfiguradas algunas temáticas que constituyeron géneros establecidos, como la novela romántica.

La chick-lit habilita la apertura a una gama de matices mucho más amplia y que abarca experiencias que no limitan a la mujer a situarse en la posición de víctima dependiente del protagonista masculino para definir su valía. Por el contrario, este tipo de literatura - frecuentemente en clave humorística - presentan a una mujer enfrentándose al mundo y a las dificultades que el mundo le plantea, precisamente, por su condición de mujer.

Me pregunto cómo sería leer una nueva versión de Madame Bovary escrita por una mujer.

---

Ampliemos el rango a todo nuestro dataset. A los diez mil libros indexados. Y busquemos cuáles son los veinte autores más indexados, y cuántos de ellos son mujeres. Y hagamos el mismo ejercicio con nuestro subconjunto.

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/006_total_authors.png" | relative_url }}">
</p>
<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/006_2009to2013_authors.png" | relative_url }}">
</p>

---

No deja de ser llamativo que una de las etiquetas más empleadas sea la de ‘audiobook’, puesto que nos permite inferir cuestiones relativas al modo de consumo de libros. Esta etiqueta en una progresión temporal acompaña y replica la misma tendencia de cantidad de libros indexados año a año:

<p align='center'>
<img class="u-max-full-width" src="{{ "/assets/images/007_audiobook.png" | relative_url }}">
</p>

Otra forma en la que podemos afirmar que el consumo está pautado por el mercado es la retroalimentación que se verifica entre la industrial editorial y la cinematográfica. Si tomamos los diez libros con el mejor rating del subconjunto de nuestro dataset (aquellos publicados entre 2009 y 2013), __la totalidad__ de ellos han sido adaptados al cine:

<table style="width:100%">
  <thead>
    <tr style="text-align: right;">
      <th>Title</th>
      <th>Author</th>
      <th>Pages</th>
      <th>Year</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>The Fault in Our Stars</td>
      <td>John Green</td>
      <td>313</td>
      <td>2012</td>
      <td>3841147</td>
    </tr>
    <tr>
      <td>Divergent</td>
      <td>Veronica Roth</td>
      <td>487</td>
      <td>2011</td>
      <td>3114605</td>
    </tr>
    <tr>
      <td>Catching Fire</td>
      <td>Suzanne Collins</td>
      <td>391</td>
      <td>2009</td>
      <td>2703892</td>
    </tr>
    <tr>
      <td>Mockingjay</td>
      <td>Suzanne Collins</td>
      <td>398</td>
      <td>2010</td>
      <td>2508098</td>
    </tr>
    <tr>
      <td>Gone Girl</td>
      <td>Gillian Flynn</td>
      <td>415</td>
      <td>2012</td>
      <td>2481211</td>
    </tr>
    <tr>
      <td>The Help</td>
      <td>Kathryn Stockett</td>
      <td>464</td>
      <td>2009</td>
      <td>2288746</td>
    </tr>
    <tr>
      <td>Fifty Shades of Grey</td>
      <td>E.L. James</td>
      <td>356</td>
      <td>2011</td>
      <td>2079768</td>
    </tr>
    <tr>
      <td>Me Before You</td>
      <td>Jojo Moyes</td>
      <td>369</td>
      <td>2012</td>
      <td>1249589</td>
    </tr>
    <tr>
      <td>Insurgent</td>
      <td>Veronica Roth</td>
      <td>525</td>
      <td>2012</td>
      <td>1243928</td>
    </tr>
    <tr>
      <td>The Maze Runner</td>
      <td>James Dashner</td>
      <td>384</td>
      <td>2009</td>
      <td>1160160</td>
    </tr>
  </tbody>
</table>


---

Entonces, ¿qué conclusiones podemos extraer?

En principio, afirmar que sin lugar a dudas los criterios del mercado son los que rigen el consumo de libros. Y que la categoría académica de ‘clásico’ se ha modificado: que un libro adquiera dicho estatus ya no depende de su capacidad de sobrevivir a lo largo del tiempo sin perder el capital simbólico que le es dado. Los libros mejor valorados en Goodreads son de publicación reciente. Y, además, pertenecen a géneros o subgéneros literarios que, por su escasa o nula historicidad y por ser derivaciones mixtas de géneros previos, aún no cuentan con criterios establecidos. El único de los que podríamos considerar tradicionales es el de ciencia ficción. Que, como sabemos, ha sufrido modificaciones y derivaciones desde la segunda mitad del siglo XX en adelante. Un género, de por sí, ya bastante difícil de encasillar o limitar.

La participación cada vez mayor de mujeres resulta evidente y al mismo tiempo relevante. Cada vez más mujeres (y, detalle no menor) jóvenes se abren paso en la industria, editando libros para que sean leídos también por mujeres. Libros que reconfiguran tópicos clásicos como el romance o la condición femenina en el mundo contemporáneo. Este hecho es alentador porque reafirma orientaciones políticas que ya tienen lugar en el ámbito social.

Es probable que la Emma Bovary del siglo XXI nunca visite la botica de Homais para adquirir arsénico y acabar con su propia vida.
