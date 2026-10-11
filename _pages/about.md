---
layout: about
title: About
permalink: /
nav: false
nav_order: 1
subtitle: PhD Student in Computer Science · University of Maryland, Baltimore County
selected_papers: false
social: false
profile:
  image: ehs-noo.jpg
---

I am a PhD student in Computer Science at the University of Maryland, Baltimore County (UMBC). My research focuses on computer graphics, particularly physics-based animation and fluid simulation. I am interested in developing computational methods for simulating complex physical phenomena and creating realistic, visually compelling animations.

My broader research interests include computer vision, machine learning, and the intersection of graphics and vision.

<nav style="display: flex; flex-wrap: wrap; column-gap: 1rem; row-gap: 0.5rem" aria-label="Professional and contact links">
  <a href="mailto:{{ site.data.socials.email | escape }}">Email</a>
  <a href="https://github.com/{{ site.data.socials.github_username | escape }}">GitHub</a>

{% if site.data.profile.linkedin %}
<a href="{{ site.data.profile.linkedin }}">LinkedIn</a>
{% endif %}

{% if site.data.profile.google_scholar %}
<a href="{{ site.data.profile.google_scholar }}">Google Scholar</a>
{% endif %}

{% if site.data.profile.orcid %}
<a href="{{ site.data.profile.orcid }}">ORCID</a>
{% endif %}

{% if site.data.profile.cv_pdf %}
<a href="{{ site.data.profile.cv_pdf | relative_url }}">CV (PDF)</a>
{% endif %}
</nav>

## Selected Publications

<p><a href="{{ '/publications/' | relative_url }}" aria-label="More publications">More →</a></p>

{% assign selected_publications = site.data.publications | where: "selected", true %}
{% if selected_publications.size > 0 %}
{% for publication in selected_publications %}
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
<article class="my-5 flex flex-col gap-5 border-b pb-5 md:flex-row">
  {% if youtube_id %}
  <a class="block w-full shrink-0 md:w-56" href="{{ youtube_link | escape }}" aria-label="Watch the video for {{ publication.title | escape }}">
    <img
      class="aspect-video w-full object-cover"
      src="https://img.youtube.com/vi/{{ youtube_id | escape }}/0.jpg"
      alt="Video thumbnail for {{ publication.title | escape }}"
      loading="lazy"
    >
    <span aria-hidden="true">▶ Watch video</span>
  </a>
  {% elsif publication.thumbnail %}
  <img
    class="aspect-video w-full shrink-0 object-cover md:w-56"
    src="{{ publication.thumbnail | relative_url }}"
    alt="{{ publication.thumbnail_alt | default: publication.title | escape }}"
    loading="lazy"
  >
  {% endif %}
  <div>
    <h3>{{ publication.title | escape }}</h3>
    {% if publication.authors %}<p>{{ publication.authors | join: ", " | escape }}</p>{% endif %}
    {% if publication.venue or publication.year %}
    <p>
      {{ publication.venue | escape }}{% if publication.venue and publication.year %}, {% endif %}{{ publication.year | escape }}
    </p>
    {% endif %}
    {% if publication.description %}<p>{{ publication.description | escape }}</p>{% endif %}
    <p class="flex flex-wrap gap-x-3">
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

## Selected Teaching

<p><a href="{{ '/teaching/' | relative_url }}" aria-label="More teaching information">More →</a></p>

{% assign selected_teaching = site.data.teaching | where: "selected", true %}
{% if selected_teaching.size > 0 %}
{% for course in selected_teaching %}
<article class="my-4 border-b pb-4">
  <h3>{{ course.title | escape }}</h3>
  <p>
    {{ course.role | escape }}{% if course.institution %}, {{ course.institution | escape }}{% endif %}{% if course.semester %} · {{ course.semester | escape }}{% endif %}
  </p>
  {% if course.description %}<p>{{ course.description | escape }}</p>{% endif %}
  {% if course.url %}<p><a href="{{ course.url | escape }}">Course website</a></p>{% endif %}
</article>
{% endfor %}
{% else %}
<p>Teaching information will be added as it becomes available.</p>
{% endif %}
