---
title: "[Blog]10. Jekyll의 HTML 활용"
excerpt: "블로그에서 댓글 만들기, 검색엔진 연동, 파비콘(favicon) 붙이기 방법을 배운다."

sort_key : 10
categories:
  - Blog
tags:
  - [Blog-팁, MMistakes, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-10
last_modified_at: 2025-10-16
---
## 시작하며
⠀자, 이제 열심히 배운 지식으로 블로그를 수정해 봅니다. HTML 문법에 대해 이해가 필요하다면 [초보용](/blog/blog-3-newbie-html/)과 [고수용](/blog/blog-7-hard-html-and-liquid/)이 준비되어 있습니다.

## 댓글 달기
⠀댓글 기능을 만드는 건 스스로 코드를 만들어 하기에는 조금 복잡하기 때문에 보통은 댓글 기능을 제공해주는 플랫폼을 이용합니다. 쉽고 편한 방법을 원하신다면 utterances나 disqus같은 댓글 플랫폼을 찾아보시면 되겠습니다. 

⠀만약, 어려운 길이지만 스스로 댓글 시스템을 만들고 싶다면, 자세한 건 [댓글 만드는 포스트](/blog/blog-14-creating-comment-system/)에서 확인하십시오.

## 검색엔진 연동
⠀검색엔진 연결할 때 `head.html`을 사용합니다. 자세한 건 후에 다루겠습니다.

## 파비콘(favicon) 붙이기
⠀Favicon(로고같은 거) 붙일 때도 사용합니다.

⠀그냥 <https://realfavicongenerator.net/>에서 하라는 대로 하면 되는 줄 알았는데 안 되서 별짓을 다 했습니다.

```html
<!-- insert favicons. use https://realfavicongenerator.net/ -->
<!-- iOS 홈 화면 이름(추가 경고 해결용) -->
<meta name="apple-mobile-web-app-title" content="당신의 사이트명">

<!-- Favicon (캐시버스터 포함) -->
<link rel="icon" type="image/png" sizes="32x32" href="{{ '/willow-blog-favicon/favicon-32x32.png?v=2' | relative_url }}">
<link rel="icon" type="image/png" sizes="16x16" href="{{ '/willow-blog-favicon/favicon-16x16.png?v=2' | relative_url }}">
<link rel="icon" type="image/png" sizes="96x96" href="{{ '/willow-blog-favicon/favicon-96x96.png?v=2' | relative_url }}">
<link rel="icon" type="image/svg+xml" href="{{ '/willow-blog-favicon/favicon.svg?v=2' | relative_url }}">
<link rel="shortcut icon" href="{{ '/willow-blog-favicon/favicon.ico?v=2' | relative_url }}">
<link rel="apple-touch-icon" sizes="180x180" href="{{ '/willow-blog-favicon/apple-touch-icon.png?v=2' | relative_url }}">
<link rel="manifest" href="{{ '/willow-blog-favicon/site.webmanifest?v=2' | relative_url }}">

<!-- (선택) 사파리 핀 탭 -->
<link rel="mask-icon" href="{{ '/willow-blog-favicon/safari-pinned-tab.svg?v=2' | relative_url }}" color="#5bbad5">
```
⠀사이트에서 주는 파일에 더해 16x16, 32x32까지 만들어서 저장하고, `site.webmanifest`파일에 밑에 보이는 바와 같이 front matter까지 붙였더니 됩니다. <span style='font-family:OngleipParkDahyeon'>빨간줄까지 뜨지만 귀찮으므로 그냥 이렇게 했습니다.</span>
```json
---
---
{
  "name": "가려 꺾은 묏버들",
  "short_name": "Willow Blog",
  "start_url": "{{ '/' | relative_url }}",
  "icons": [
    { "src": "{{ '/willow-blog-favicon/web-app-manifest-192x192.png?v=2' | relative_url }}", "sizes": "192x192", "type": "image/png" },
    { "src": "{{ '/willow-blog-favicon/web-app-manifest-512x512.png?v=2' | relative_url }}", "sizes": "512x512", "type": "image/png" }
  ],
  "theme_color": "#ffffff",
  "background_color": "#ffffff",
  "display": "standalone"
}
```

## 마무리
⠀복잡하면 그냥 제 repository에서 복붙하시면 됩니다. 버그는 댓글이나 메일로 물어보시면 열심히 생각해 보겠습니다.