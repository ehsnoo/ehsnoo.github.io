---
layout: default
title: Home
permalink: /
nav: false
nav_order: 1
subtitle: PhD Student in Computer Science · University of Maryland, Baltimore County
selected_papers: false
social: false
profile:
  image: ehs-noo.jpg
---

<link rel="stylesheet" href="{{ '/assets/css/academic-layout.css' | relative_url }}">

<div class="academic-profile">
<header class="academic-intro">
  <h1>{{ site.first_name | escape }} {{ site.last_name | escape }}</h1>
</header>
<figure class="academic-photo">
  <img class="profile-photo" src="{{ page.profile.image | prepend: '/assets/img/' | relative_url }}" alt="Portrait of {{ site.first_name | escape }} {{ site.last_name | escape }}">
</figure>
<p class="academic-position">{{ page.subtitle | escape }}</p>
<div class="academic-biography" markdown="1">

I am a PhD student in Computer Science at the University of Maryland, Baltimore County (UMBC). My research focuses on computer graphics, particularly physics-based animation and fluid simulation. I am interested in developing computational methods for simulating complex physical phenomena and creating realistic, visually compelling animations.

My broader research interests include computer vision, machine learning, and the intersection of graphics and vision.

</div>
<aside class="academic-sidebar" aria-label="Profile sidebar">
<nav class="contact-links" aria-label="Professional and contact links">
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
<a href="{{ site.data.profile.cv_pdf | relative_url }}">CV</a>
{% endif %}
</nav>
{% assign selected_teaching = site.data.teaching | where: "selected", true %}
<section class="teaching-sidebar" aria-labelledby="teaching-heading">
  <h2 id="teaching-heading">Teaching</h2>
  {% if selected_teaching.size > 0 %}
  {% for course in selected_teaching %}
  <p class="teaching-course">{{ course.title | escape }}{% if course.semester %} [{{ course.semester | escape }}]{% endif %}</p>
  {% endfor %}
  {% else %}
  <p class="teaching-course">Teaching information will be added as it becomes available.</p>
  {% endif %}
  {% if site.data.teaching_examples.size > 0 %}
  <p class="teaching-disclaimer">Fictional demonstrations:</p>
  {% for course in site.data.teaching_examples %}
  <p class="teaching-course"><span>{{ course.title | escape }}</span> [{{ course.semester | escape }}]</p>
  {% endfor %}
  {% endif %}
</section>
</aside>
</div>

## Selected Publications

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
<article class="publication-entry">
  {% if youtube_id %}
  <a class="publication-thumbnail" href="{{ youtube_link | escape }}" aria-label="Watch the video for {{ publication.title | escape }}">
    <img class="publication-image" src="https://img.youtube.com/vi/{{ youtube_id | escape }}/0.jpg" alt="Video thumbnail for {{ publication.title | escape }}" loading="lazy">
    <span aria-hidden="true">▶ Watch video</span>
  </a>
  {% elsif publication.thumbnail %}
  <img class="publication-image publication-thumbnail" src="{{ publication.thumbnail | relative_url }}" alt="{{ publication.thumbnail_alt | default: publication.title | escape }}" loading="lazy">
  {% endif %}
  <div class="publication-details">
    <h3>{{ publication.title | escape }}</h3>
    {% if publication.authors %}<p>{{ publication.authors | join: ", " | escape }}</p>{% endif %}
    {% if publication.venue or publication.year %}<p>{{ publication.venue | escape }}{% if publication.venue and publication.year %}, {% endif %}{{ publication.year | escape }}</p>{% endif %}
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
  {% if publication.thumbnail %}<img class="publication-image publication-thumbnail" src="{{ publication.thumbnail | relative_url }}" alt="{{ publication.thumbnail_alt | escape }}" loading="lazy">{% endif %}
  <div class="publication-details">
    <p><strong>Sample — Not a real publication</strong></p>
    <h3>{{ publication.title | escape }}</h3>
    <p>{{ publication.authors | join: ", " | escape }}</p>
    <p>{{ publication.venue | escape }}, {{ publication.year | escape }}</p>
    <p>{{ publication.description | escape }}</p>
    <p class="publication-links" aria-label="Illustrative, nonfunctional publication controls"><span>Paper</span><span>Video</span><span>Code</span></p>
  </div>
</article>
{% endfor %}
{% endif %}

<p class="all-publications"><a href="{{ '/publications/' | relative_url }}" aria-label="View all publications">All Publications →</a></p>
