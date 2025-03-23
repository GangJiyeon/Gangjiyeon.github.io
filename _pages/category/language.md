---
title: "language"
layout: archive
permalink: /language
author_profile: true
types: posts
---

{% assign posts = site.categories['language']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}