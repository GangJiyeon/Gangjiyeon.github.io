---
title: "dev-log"
layout: archive
permalink: categories/dev-log
author_profile: true
types: posts
---

{% assign posts = site.categories.dev-log %}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}