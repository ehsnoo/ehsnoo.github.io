---
layout: page
permalink: /teaching/
title: Teaching
description: Teaching experience and course information.
nav: true
nav_order: 4
---

{% if site.data.teaching.size > 0 %}
{% assign courses = site.data.teaching | sort: "semester" | reverse %}
{% for course in courses %}
<article class="my-5 border-b pb-5">
  <h2>{{ course.title | escape }}</h2>
  <p>{{ course.role | escape }}{% if course.institution %}, {{ course.institution | escape }}{% endif %}{% if course.semester %} · {{ course.semester | escape }}{% endif %}</p>
  {% if course.description %}<p>{{ course.description | escape }}</p>{% endif %}
  {% if course.url %}<p><a href="{{ course.url | escape }}">Course website</a></p>{% endif %}
</article>
{% endfor %}
{% else %}
<p>Teaching information will be added as it becomes available.</p>
{% endif %}

{% if site.data.teaching_examples.size > 0 %}
## Teaching Examples — Demonstration Only

{% for course in site.data.teaching_examples %}
<article class="my-5 border-b pb-5">
  <p><strong>Sample — Not an actual teaching appointment</strong></p>
  <h2>{{ course.title | escape }}</h2>
  <p>{{ course.role | escape }}, {{ course.institution | escape }} · {{ course.semester | escape }}</p>
</article>
{% endfor %}
{% endif %}
