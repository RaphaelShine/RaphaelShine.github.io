---
title: "[Blog]6. 초보용 CSS 설명"
excerpt: "블로그를 위해 CSS의 기본 문법(선택자(selector), 속성(property))을 알아본다."

sort_key : 6
categories:
  - Blog
tags:
  - [Blog-뼈대, 프런트엔드, Blog-초보]

header:
  overlay_image: https://1000logos.net/wp-content/uploads/2020/09/CSS-Logo-2011.png
  overlay_filter: 0.3
  caption: "CSS3 logo"

toc: true
toc_sticky: true

date: 2025-10-09
last_modified_at: 2025-10-14
---
## 시작하며
⠀CSS는 HTML을 꾸며주는 아이입니다. 가끔 인터넷이 잘 안될 때 사이트에 들어갔다가 새하얀 창에 맹한 글씨만 뜬 걸 보신 적 있으십니까? CSS가 없는 HTML의 처참한 쌩얼입니다. CSS는 HTML에서 \<style>을 써서 작성할 수도 있고 \<tag style="">로 넣을 수도 있고 따로 `.css`나 `.scss`, `.sass` 등의 확장자를 사용해 작성할 수 있습니다. 우리는 포스트를 작성할 때 주로 \<tag style="">를 이용하고 사이트 전체를 스타일링 할 때 `.scss`를 이용할 예정입니다.

CSS는 대충
```scss
selector {
  property: value;
}
```
이렇게 생겼습니다.

⠀선택자(selector)로 HTML의 구성요소를 지목해서 CSS 속성(property)을 달아주는 겁니다. HTML 속성은 attribute로, property에 대응하는 게 아니라 selector에 대응하여 CSS에서 attribute를 가지고 HTML 구성요소를 지목하게 됩니다.

## 선택자
⠀CSS로 HTML의 어느 부분을 꾸밀지 선택합니다. 일단 예시를 드립니다.
```html
<div class="example-1">
  <div class="example-division-1">
    <h4>1번 지원자</h4>
    안녕하십니까!
  </div>
  <div class="example-division-2">
    <h4>2번 지원자</h4>
    안녕하세요??
  </div>
  <div class="example-division-3">
    <h4 class="class-example">3번 지원자</h4>
    안녕하십니까...
  </div>
</div>
<style>
  .example-1 {
    background-color: black;
  }
  .example-1 h4 {
    color: blue;
  }
  .example-1 h4.class-example {
    color: red;
  }
</style>
```
<div class="example-1">
  <div class="example-division-1">
    <h4>1번 지원자</h4>
    안녕하십니까!
  </div>
  <div class="example-division-2">
    <h4>2번 지원자</h4>
    안녕하세요??
  </div>
  <div class="example-division-3">
    <h4 class="class-example">3번 지원자</h4>
    안녕하십니까...
  </div>
</div>
<style>
  .example-1 {
    background-color: black;
  }
  .example-1 h4 {
    color: blue;
  }
  .example-1 h4.class-example {
    color: red;
  }
</style>
<br>
⠀CSS에서 tag명을 이용해 특정할 때는 태그명을 그대로 적고, class명을 이용해 특정할 때는 `.`을 찍고 적으면 됩니다. 합집합으로 선택 시에는 `,`로 연결하고, 붙여서 연결하면 상위tag 고려 없이 하나의 tag에 다 담긴 것만 선택됩니다. 띄어쓰기로 연결하면 어떤 선택자에 더 감싸져야 하는지도 지정할 수 있습니다.

## 속성(Property)
⠀CSS는 이게 중요합니다. CSS가 결국에 건들이는 부분은 속성이 전부기 때문입니다. 이 블로그에서 모든 속성을 다룰 순 없으니 그때그때 필요한 property는 인터넷에 검색하십시오.
### color
```html
<div class="example-4">
  <div class="color-example-1">
    노랗게 노랗게 물들었네
  </div>
  <div class="color-example-2">
    빨갛게 빨갛게 물들었네
  </div>
  <div class="color-example-3">
    파랗게 파랗게 물든 하늘
  </div>
</div>
<style>
  .example-4 .color-example-1 {
    color:yellow;
  }
  .example-4 .color-example-2 {
    color:red;
  }
  .example-4 .color-example-3 {
    background-color:blue;
  }
</style>
```
<div class="example-4">
  <div class="color-example-1">
    노랗게 노랗게 물들었네
  </div>
  <div class="color-example-2">
    빨갛게 빨갛게 물들었네
  </div>
  <div class="color-example-3">
    파랗게 파랗게 물든 하늘
  </div>
</div>
<style>
  .example-4 .color-example-1 {
    color:yellow;
  }
  .example-4 .color-example-2 {
    color:red;
  }
  .example-4 .color-example-3 {
    background-color:blue;
  }
</style>

### font-size
```html
<div class="example-5">
  <div class="font-size-example">
    듬직듬직
  </div>
</div>
<style>
  .example-5 .font-size-example {
    font-size: 50px;
  }
</style>
```
<div class="example-5">
  <div class="font-size-example">
    듬직듬직
  </div>
</div>
<style>
  .example-5 .font-size-example {
    font-size: 50px;
  }
</style>

### font-align
⠀`center`하면 가운데,`right`하면 오른쪽 정렬됩니다.

## 우선순위
⠀CSS는 우선순위가 있어서 코드를 적어도 우선순위가 더 높은 코드가 다른 곳에서 방해하면 원하는 대로 동작할 수 없습니다. 따라서 `!important`를 붙여주어 우선순위를 높일 수 있습니다. 남발하면 안되겠죠?
```scss
@include breakpoint($small) {
  font-size: $size * 0.6 !important;
}
```
⠀이 골뱅이 친구는 화면 크기에 따라 글자 크기를 바꿔주는 친굽니다.

## 변수
SCSS는 변수를 `$변수명`으로 작성합니다. 많이 쓰는 색 같은 걸 이렇게 저장해 뒀다가 후에 수정할 때 한번에 바꿉니다.
```scss
$var: "값";
```

## 마무리
⠀CSS는 딱히 깊게 알 필요가 없다고 생각해서 이정도에서 끝내겠습니다. 이제 이론은 끝났고 다음 포스트부터는 Jekyll에 적용해 보겠습니다. 고수용도 읽어볼 자신이 있으시다면 다음 포스트로 가서 고수용도 읽어 보십시오. [아니면 그냥 적용 배우러 가기](/blog/blog-10-how-to-use-html/)