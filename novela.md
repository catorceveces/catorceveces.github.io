---
layout: page
title: "Catorce Veces - Novela"
---

<h6><center> NOVELA </center></h6>

<hr style='margin-bottom:2rem'>

{% for post in site.tags.novela limit:10 %}

<p><center><a style='color: #1E90FF; text-decoration:underline;' href="{{ post.url | relative_url }}">{{ post.title }}</a></center></p>

{{ post.content }}

<br>

{% endfor %}

<hr style='margin-top:1rem'>

<p><center><a style='color: #126AD2; text-decoration:underline;' href="/">Volver</a></center></p>
