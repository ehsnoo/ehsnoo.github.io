---
layout: academic
permalink: /publications/
title: Publications
description: Publications by Ehs Noo.
nav: true
nav_order: 3
---

{% if site.data.publications.size > 0 %}
{% assign publications = site.data.publications | sort: "year" | reverse %}
{% for publication in publications %}
{% assign youtube_id = publication.youtube_id %}
{% if youtube_id == nil and publication.video_url %}
{% if publication.video_url contains 'youtu.be/' %}
    {% assign youtube_id = publication.video_url | split: 'youtu.be/' | last | split: '?' | first | split: '&' | first %}
{% elsif publication.video_url contains 'v=' %}
    {% assign youtube_id = publication.video_url | split: 'v=' | last | split: '&' | first %}
{% elsif publication.video_url contains '/embed/' or publication.video_url contains '/shorts/' or publication.video_url contains '/live/' %}
    {% assign youtube_id = publication.video_url | split: '/' | last | split: '?' | first %}
{% endif %}
{% endif %}
{% assign youtube_link = publication.video_url %}
{% unless youtube_link %}{% assign youtube_link = 'https://www.youtube.com/watch?v=' | append: youtube_id %}{% endunless %}
<article class="publication-entry">
  {% if youtube_id %}
  <a class="publication-thumbnail" href="{{ youtube_link | escape }}" aria-label="Watch the video for {{ publication.title | escape }}">
    <img
      class="publication-image"
      src="https://img.youtube.com/vi/{{ youtube_id | escape }}/0.jpg"
      alt="Video thumbnail for {{ publication.title | escape }}"
      loading="lazy"
    >
    <span aria-hidden="true">▶ Watch video</span>
  </a>
  {% elsif publication.thumbnail %}
  <img
    class="publication-image publication-thumbnail"
    src="{{ publication.thumbnail | relative_url }}"
    alt="{{ publication.thumbnail_alt | default: publication.title | escape }}"
    loading="lazy"
  >
  {% endif %}
  <div class="publication-details">
    <h2>{{ publication.title | escape }}</h2>
    {% if publication.authors %}<p>{{ publication.authors | join: ", " | escape }}</p>{% endif %}
    {% if publication.venue or publication.year %}
    <p>
      {{ publication.venue | escape }}{% if publication.venue and publication.year %}, {% endif %}{{ publication.year | escape }}
    </p>
    {% endif %}
    {% if publication.description %}<p>{{ publication.description | escape }}</p>{% endif %}
    <p class="publication-links">
      {% if publication.paper_url %}<a href="{{ publication.paper_url | escape }}">Paper</a>{% endif %}
      {% if publication.video_url %}<a href="{{ publication.video_url | escape }}">Video</a>{% endif %}
      {% if publication.code_url %}<a href="{{ publication.code_url | escape }}">Code</a>{% endif %}
      {% if publication.bibtex_url %}<a href="{{ publication.bibtex_url | escape }}">BibTeX</a>{% endif %}
    </p>
  </div>
</article>
{% endfor %}
{% else %}
<p>Research in progress. Publications and project results will be shared here as they become available.</p>
{% endif %}

{% if site.data.publication_examples.size > 0 %}
## Layout Examples — Demonstration Only

{% for publication in site.data.publication_examples %}
<article class="publication-entry">
  {% if publication.thumbnail %}
  <img class="publication-image publication-thumbnail" src="{{ publication.thumbnail | relative_url }}" alt="{{ publication.thumbnail_alt | escape }}" loading="lazy">
  {% endif %}
  <div class="publication-details">
    <p><strong>Sample — Not a real publication</strong></p>
    <h2>{{ publication.title | escape }}</h2>
    <p>{{ publication.authors | join: ", " | escape }}</p>
    <p>{{ publication.venue | escape }}, {{ publication.year | escape }}</p>
    <p>{{ publication.description | escape }}</p>
    <p class="publication-links" aria-label="Illustrative, nonfunctional publication controls">
      <span>Paper</span>
      <span>Video</span>
      <span>Code</span>
    </p>
  </div>
</article>
{% endfor %}
{% endif %}
