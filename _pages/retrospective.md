---
title: "retrospective"
layout: archive
permalink: categories/retrospective
author_profile: true
types: posts
---

{% assign posts = site.categories.retrospective %}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}