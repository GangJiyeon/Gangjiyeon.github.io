---
title: "game development"
layout: archive
permalink: categories/game
author_profile: true
types: posts
---

{% assign posts = site.categories.game %}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}