---
layout: academic
permalink: /research/
title: Research
description: Research interests and projects of Ehs Noo.
nav: true
nav_order: 2
---

My research focuses on computer graphics, particularly physics-based animation and fluid simulation. I am interested in computational methods for simulating complex physical phenomena and creating realistic, visually compelling animations. My broader interests include computer vision, machine learning, and the intersection of graphics and vision.

Research projects and demonstrations will be added as they become available.

{% for project in site.data.research_projects %}
{% assign youtube_id = project.youtube_id %}
{% if youtube_id == nil and project.video_url %}
{% if project.video_url contains 'youtu.be/' %}
    {% assign youtube_id = project.video_url | split: 'youtu.be/' | last | split: '?' | first | split: '&' | first %}
{% elsif project.video_url contains 'v=' %}
    {% assign youtube_id = project.video_url | split: 'v=' | last | split: '&' | first %}
{% elsif project.video_url contains '/embed/' or project.video_url contains '/shorts/' or project.video_url contains '/live/' %}
    {% assign youtube_id = project.video_url | split: '/' | last | split: '?' | first %}
{% endif %}
{% endif %}
{% assign youtube_link = project.video_url %}
{% unless youtube_link %}{% assign youtube_link = 'https://www.youtube.com/watch?v=' | append: youtube_id %}{% endunless %}
<article class="my-6 border-b pb-6">
  <h2>{{ project.title | escape }}</h2>
  {% if project.status %}<p><strong>Status:</strong> {{ project.status | escape }}</p>{% endif %}
  {% if project.description %}<p>{{ project.description | escape }}</p>{% endif %}
  {% if project.image %}
  <img
    class="my-4 h-auto max-w-full"
    src="{{ project.image | relative_url }}"
    alt="{{ project.image_alt | default: project.title | escape }}"
    loading="lazy"
  >
  {% endif %}
  {% if youtube_id %}
  <p><a href="{{ youtube_link | escape }}" aria-label="Watch the video for {{ project.title | escape }}">
    <img
      class="aspect-video w-full md:max-w-xl"
      src="https://img.youtube.com/vi/{{ youtube_id | escape }}/0.jpg"
      alt="Video thumbnail for {{ project.title | escape }}"
      loading="lazy"
    >
    Watch project video
  </a></p>
  {% endif %}
  <p class="flex flex-wrap gap-x-3">
    {% if project.paper_url %}<a href="{{ project.paper_url | escape }}">Paper</a>{% endif %}
    {% if project.code_url %}<a href="{{ project.code_url | escape }}">Code</a>{% endif %}
  </p>
</article>
{% endfor %}
