---
title: Life
layout: archive
permalink: /life/
collection: life
classes: wide
---

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>

{% for post in site.categories.life %}
{% include archive-single.html %}
{% endfor %}

{% include paginator.html %}