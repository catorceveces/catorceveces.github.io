---
layout: page
title: "Catorce Veces - Proyectos"
---

<h6><center> PROYECTOS </center></h6>

<hr style='margin-bottom:2rem'>

{% for post in site.tags.proyectos limit:10 %}

<p><center><a style='color: #1E90FF; text-decoration:none;' href="{{ post.url | relative_url }}">{{ post.title }}</a></center></p>
<p> {{ post.description }}</p>

{% endfor %}

<hr style='margin-top:1rem'>

<p><center><a style='color: #126AD2; text-decoration:underline;' href="/">Volver</a></center></p>
