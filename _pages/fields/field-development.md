---
title: "Development"
layout: archive
permalink: /development/
author_profile: true
sidebar_main: true
---

***
{% assign categorylist = site.fields.development %}
{% for a_category in categorylist %} {% include archive-category.html category="Development" type=page.entries_layout %} {% endfor %}
<!--
{% assign categorylist = site.fields.development %}
{% for a_category in categorylist %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}-->