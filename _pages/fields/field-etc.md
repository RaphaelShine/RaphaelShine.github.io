---
title: "Etc"
layout: archive
permalink: /etc/
author_profile: true
sidebar_main: true
---

***
<!--노가다를 해야겠다... -->
{% assign devcats = "Blog" | split: "," %}
{% for devcat in devcats %}
  <h3><a href="/etc/{{devcat}}">{{devcat}}</a></h3>
  <hr>
  {% assign posts = site.categories[devcat] %}
  {% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
  <br>
{% endfor %}
