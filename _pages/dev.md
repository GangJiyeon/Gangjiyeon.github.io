---
title: "study-dev"
layout: archive
permalink: categories/dev
author_profile: true
types: posts
---

{% assign posts = site.categories.language %}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}