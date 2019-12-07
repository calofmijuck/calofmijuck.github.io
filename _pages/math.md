---
title: Mathematics
layout: archive
permalink: /math/
collection: math
classes: wide
---

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>

{% for post in site.categories.math %}
{% include archive-single.html %}
{% endfor %}

{% include paginator.html %}