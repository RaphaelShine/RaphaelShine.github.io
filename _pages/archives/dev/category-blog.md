---
title: "Blog"
layout: archive
permalink: /development/blog/
author_profile: true
sidebar_main: true
---

<!-- 공백이 포함되어 있는 카테고리 이름의 경우 site.categories.['a b c'] 이런식으로! -->

***
<!--필요하다면 여기서 하드코딩으로 세부카테고리 만들고 만다.-->
{% assign posts = site.categories.Blog | sort: "sort_key" | reverse %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}