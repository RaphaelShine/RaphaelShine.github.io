---
title: "Etc"
layout: archive
permalink: /etc/
author_profile: true
sidebar_main: true
---

***

{% assign categorylist = site.fields.ect %}
{% for a_category in categorylist %} {% include archive-category.html category="Etc" type=page.entries_layout %} {% endfor %}