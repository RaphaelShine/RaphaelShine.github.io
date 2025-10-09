---
title: "[Blog]6. 초보용 CSS 설명"
excerpt: "CSS의 기본 문법을 알아본다."

sort_key : 6
categories:
  - Blog
tags:
  - [Blog-뼈대부터, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-09
last_modified_at: 2025-10-09
---
## 시작하며
⠀CSS는 HTML을 꾸며주는 아이입니다. 가끔 인터넷이 잘 안될 때 사이트에 들어갔다가 새하얀 창에 맹한 글씨만 뜬 걸 보신 적 있으십니까? CSS가 없는 HTML의 처참한 쌩얼입니다. CSS는 HTML에서 \<style>을 써서 작성할 수도 있고 \<tag style="">로 넣을 수도 있고 따로 `.css`나 `.scss`, `.sass` 등의 확장자를 사용해 작성할 수 있습니다. 우리는 포스트를 작성할 때는 \<tag style="">를 이용해 바로 넣기도 하고 사이트 전체를 스타일링 할 때 `.scss`를 이용할 예정입니다.

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
    <h4>3번 지원자</h4>
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
</style>
```
<div class="example-1">
  <div class="example-division-1">
    <h4>1번 지원자</h4>
    안녕하십니까!
  </div>
  <div class="example-division-2">
    <h4>2번 지원자</h4>
    안녕하세요...
  </div>
  <div class="example-division-3">
    <h4>3번 지원자</h4>
    안녕하십니까??
  </div>
</div>
<style>
  .example-1 {
    background-color: black;
  }
  .example-1 h4 {
    color: blue;
  }
  .example-1 .example-division-1,
  .example-1 .example-division-3 {
    font-size: 20px;
  }
</style>
<br>
⠀CSS에서 tag명을 이용해 특정할 때는 태그명을 그대로 적고, class명을 이용해 특정할 때는 `.`을 찍고 적으면 됩니다. 합집합으로 선택 시에는 `,`로 연결하고, 교집합으로 선택 시에는 띄어쓰기로 연결합니다. 특정 선택자와 다른 선택자를 갖고 있는데 그 둘 사이의 관계가 어떻게 되는지까지 고려하여 선택할 수도 있습니다.

## 속성(Property)
⠀CSS는 이게 중요합니다. CSS가 결국에 건들이는 부분은 속성이 전부기 때문입니다.
### width, height
```html
<div class="example-4">
  <div class="wid-hei-example">
    집이 찌부가 되다.
  </div>
  <div>
    날벼락 맞다.
  </div>
</div>
<style>
  .example-4 .wid-hei-example {
    width: 120px;
    height: 100px;
  }
</style>
```
<div class="example-4">
  <div class="wid-hei-example">
    집이 찌부가 되다.
  </div>
  <div>
    날벼락 맞다.
  </div>
</div>
<style>
  .example-4 .wid-hei-example {
    width: 120px;
    height: 10px;
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

### 테두리

```html
<div class="example-6">
  <span class="spectrum-example red-example">빨</span>
  <span class="spectrum-example orange-example">주</span>
  <span class="spectrum-example yellow-example">노</span>
  <span class="spectrum-example green-example">초</span>
</div>
<style>
  .example-6 .spectrum-example {
    color: black;
  }
  .example-6 .red-example {
    padding: 2px;
    background-color: red;
  }
  .example-6 .orange-example {
    padding: 4px;
    background-color: orange;
  }
  .example-6 .yellow-example {
    padding: 8px;
    background-color: yellow;
  }
  .example-6 .green-example {
    padding: 16px;
    background-color: green;
  }
</style>
```
<div class="example-6">
  <span class="spectrum-example red-example">빨</span>
  <span class="spectrum-example orange-example">주</span>
  <span class="spectrum-example yellow-example">노</span>
  <span class="spectrum-example green-example">초</span>
</div>
<style>
  .example-6 .spectrum-example {
    color: black;
  }
  .example-6 .red-example {
    padding: 2px;
    background-color: red;
  }
  .example-6 .orange-example {
    padding: 4px;
    background-color: orange;
  }
  .example-6 .yellow-example {
    padding: 8px;
    background-color: yellow;
  }
  .example-6 .green-example {
    padding: 16px;
    background-color: green;
  }
</style>
테두리는 padding, border, margin이 있습니다.

## 마무리
⠀CSS는 딱히 깊게 알 필요가 없다고 생각해서 이정도에서 끝내겠습니다. 이제 이론은 끝났고 다음 포스트부터는 Jekyll에 적용해 보겠습니다. 고수용도 읽어볼 자신이 있으시다면 고수용도 읽어 보십시오. [그냥 적용 배우러 가기]()