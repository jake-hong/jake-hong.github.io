---
layout: archive
title: "TIL (Today I Learned)"
permalink: /til/
author_profile: true
sidebar:
  nav: "main"
---

{% for post in site.til %}
  {% include archive-single.html %}
{% endfor %}
