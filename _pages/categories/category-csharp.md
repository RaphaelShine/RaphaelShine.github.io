---
title: "C#"
layout: archive
permalink: /development/csharp/
author_profile: true
sidebar_main: true

fields: "development"
---

<!-- 공백이 포함되어 있는 카테고리 이름의 경우 site.categories.['a b c'] 이런식으로! -->

***

{% assign posts = site.categories.Blog %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}