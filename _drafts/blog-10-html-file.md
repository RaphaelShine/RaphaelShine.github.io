---
title: "[Blog]10. Jekyll의 HTML 파일"
excerpt: "Jekyll의 HTML 파일들(includes, layouts)에 대해 구체적으로 정리한다."

sort_key : 10
categories:
  - Blog
tags:
  - [Blog-구체적으로, MMistakes]

toc: true
toc_sticky: true

date: 2025-10-08
last_modified_at: 2025-10-08
---
## 시작하며
⠀자, 드디어 구체적인 파일들의 역할과, 이 파일들을 어떻게 고쳤기에 본 블로그의 모양새가 되었는지 파해칠 때가 왔습니다. 두근두근 하도록 하십시오.

⠀수정사항 대부분이 HTML이라 이 포스트가 상당히 길어질 예정입니다.

# `_includes/`
⠀`analytics-providers/`, `footer/`, `head/`, `after-contnt.html`는 알 필요 없습니다.
## `comments-providers/`
⠀댓글 만들고 돌아오겠습니다.
## `search/`
⠀Blog 카테고리 완결하고 검색엔진 등록하고 돌아오겠습니다.
## `analytics.html`
⠀analytics-provider를 선택합니다. `_config.yml`에서 설정된 provider를 case문을 이용해 선택해 `analytics-providers/`합니다.
## `archive-category.html`


# `_layouts/`
##