---
title: "[Blog]11. Jekyll의 YAML 활용"
excerpt: "블로그에서 포스트 정렬하는 법, 제목 뒤에 이미지 띄우는 법을 배운다."

sort_key : 11
categories:
  - Blog
tags:
  - [Blog-팁, MMistakes, Blog-날먹, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-09
last_modified_at: 2025-10-16
---
## 활용법
⠀YAML 문법에 대해 이해가 필요하다면 [여기](/blog/blog-5-newbie-yaml/)에 준비되어 있습니다.

## 포스트 정렬 기준 설정
⠀기본적으로 나열되는 순서가 날짜순이므로 포스트를 마구 찍어내다 보면 순서를 조정하고 싶을 수 있습니다.

⠀front matter에 변수를 하나 만듭니다.
```yml
sort_key : 11
```
⠀포스트를 나열하는 Markdown 파일에서 다음과 같이 `sort:""` filter에 변수명을 넣어주면 됩니다.
```liquid
{% raw %}{% assign posts = site.categories.Blog | sort: "sort_key" | reverse %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}{% endraw %}
```

## 제목 뒤쪽에 이미지 띄우기
⠀제목 뒤에 이미지 뜨면 좀 있어 보입니다.

⠀front matter에 다음과 같이 작성합니다.
```yml
header:
  overlay_image: # 이미지 src
  overlay_filter: 0.3 # 검게 0부터 1까지
  caption: "설명(우측하단)"
```
⠀수정을 원한다면 [`hero.html`](/blog/blog-10-html-file/#page__herohtml)을 수정하십시오.