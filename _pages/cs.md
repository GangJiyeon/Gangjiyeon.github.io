---
title: "cs"
layout: archive
permalink: categories/cs
author_profile: true
types: posts
---

{% assign posts = site.categories.cs %}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}