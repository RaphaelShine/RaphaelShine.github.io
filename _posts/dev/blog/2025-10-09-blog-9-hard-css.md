---
title: "[Blog]9. 고수용 CSS 설명"
excerpt: "CSS의 기본 문법과 before, after, count 등의 기능, 여러 속성(property)과 CSS의 변수, 함수(function, mixin), 조건문(if), 반복문(for) 사용 방법을 알아본다."

sort_key : 9
categories:
  - Blog
tags:
  - [Blog-뼈대, 프런트엔드, Blog-고수]

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
⠀CSS는 HTML을 꾸며주는 아이입니다. 가끔 인터넷이 잘 안될 때 사이트에 들어갔다가 새하얀 창에 맹한 글씨만 뜬 걸 보신 적 있으십니까? CSS가 없는 HTML의 처참한 쌩얼입니다. CSS는 정말 단순하기 때문에 템플릿 가져와서 수정만 하는 수준에서는 딱히 공부 대충 했다고 티 안납니다. 그러니 우리는 고수용 포스트긴 해도 대충대충 기초적인 것만 짚고 넘어가도 되겠습니다.

⠀CSS는 HTML에서 \<style>을 써서 작성할 수도 있고 \<tag style="">로 넣을 수도 있고 따로 `.css`나 `.scss`, `.sass` 등의 확장자를 사용해 작성할 수 있습니다. SCSS나 Sass는 CSS의 전처리기라고 합니다. CSS에는 변수, 함수, 조건문, 반복문 등이 없는데, 전처리기는 이것들을 작성할 수 있습니다. 작성한 변수나 함수를 처리해 알아서 CSS로 만들어주는 원리입니다. 여러 전처리기가 있지만 우리는 SCSS를 사용할 예정입니다.

CSS는 대충
```scss
selector {
  property: value;
}
```
이렇게 생겼습니다.

⠀선택자(selector)로 HTML의 구성요소를 지목해서 CSS 속성(property)을 달아주는 겁니다. HTML 속성은 attribute로, property에 대응하는 게 아니라 selector에 대응하여 CSS에서 attribute를 가지고 HTML 구성요소를 지목하게 됩니다.

## 선택자
### 선택자 문법
⠀A와 B라는 선택자가 있다고 했을 때, 각각의 관계를 특정하여 스타일을 정할 수 있습니다.
```scss
A, B {
  property: value;
}
```
```html
<A>A도 선택</A>
<B>B도 선택</B>
```

```scss
AB {
  property: value;
}
```
```html
<A B>A와 B를 동시에 만족</A B>
```

```scss
A>B {
  property: value;
}
```
```html
<A><B>A 바로 밑에 B</B></A>
```

```scss
A B {
  property: value;
}
```
```html
<A><C><B>A 밑 어딘가에 B</B></C></A>
```

```scss
A+B {
  property: value;
}
```
```html
<A></A>
<B>A 다음에 오는 B</B>
```

```scss
A~B {
  property: value;
}
```
```html
<A></A>
<B>A 다음에 오는 모든 B</B>
<C></C>
<B>A 다음에 오는 모든 B</B>
```

### 의사 클래스
⠀특별한 상태를 선택할 때 사용합니다. 아래는 대표적인 상태들입니다.
|:---:|---|
|:hover|마우스 올림|
|:active|클릭중|
|:focus|tab키 조준|
|:link|안 눌러 본 링크|
|:visited|눌러 본 링크|
⠀이런 식으로 `:`를 붙여 사용합니다.
```scss
A:hover {
  property: value;
}
```

### before, after
⠀before와 after는 각각 선택된 부분의 앞과 뒤에 무언가를 붙이는 **의사요소**입니다. 의사요소는 `::`를 붙입니다.
```html
<div class="example-2">
  <div class="example-division-1">
    <h4>1번</h4>
    안녕하십니까!
  </div>
  <div class="example-division-2">
    <h4>2번</h4>
    안녕하세요??
  </div>
  <div class="example-division-3">
    <h4>3번</h4>
    안녕하십니까...
  </div>
</div>
<style>
  .example-2 {
    background-color: black;
  }
  .example-2 h4 {
    color: blue;
  }
  .example-2 h4::after {
    content: " 지원자"
  }
</style>
```
<div class="example-2">
  <div class="example-division-1">
    <h4>1번</h4>
    안녕하십니까!
  </div>
  <div class="example-division-2">
    <h4>2번</h4>
    안녕하세요??
  </div>
  <div class="example-division-3">
    <h4>3번</h4>
    안녕하십니까...
  </div>
</div>
<style>
  .example-2 {
    background-color: black;
  }
  .example-2 h4 {
    color: blue;
  }
  .example-2 h4::after {
    content: " 지원자"
  }
</style>
<br>
⠀content 속성을 넣으면 content가 출력됩니다. after 안에도 after의 다른 속성(color, font-size 등)을 넣어줄 수 있습니다.

### count()
⠀그런데 똑같이 반복되는 것은 아니지만 앞의 번호도 일정한 규칙으로 반복되고 있습니다. count()를 이용하면 CSS에서도 간단한 숫자세기를 해줄 수 있습니다.
```html
<div class="example-3">
  <div class="example-division-1">
    <h4>번</h4>
    안녕하십니까!
  </div>
  <div class="example-division-2">
    <h4>번</h4>
    안녕하세요??
  </div>
  <div class="example-division-3">
    <h4>번</h4>
    안녕하십니까...
  </div>
</div>
<style>
  .example-3 {
    background-color: black;
    counter-reset: h4;
  }
  .example-3 h4 {
    color: blue;
  }
  .example-3 h4::before {
    counter-increment: h4;
    content: counter(h4)
  }
  .example-3 h4::after {
    content: " 지원자"
  }
</style>
```
<div class="example-3">
  <div class="example-division-1">
    <h4>번</h4>
    안녕하십니까!
  </div>
  <div class="example-division-2">
    <h4>번</h4>
    안녕하세요??
  </div>
  <div class="example-division-3">
    <h4>번</h4>
    안녕하십니까...
  </div>
</div>
<style>
  .example-3 {
    background-color: black;
    counter-reset: h4;
  }
  .example-3 h4 {
    color: blue;
  }
  .example-3 h4::before {
    counter-increment: h4;
    content: counter(h4)
  }
  .example-3 h4::after {
    content: " 지원자"
  }
</style>

## 속성(Property)
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
테두리 종류도 여러개라 padding, border, margin이 있습니다.

## 함수
프로그래밍에서 함수는 동작들의 묶음인데, SCSS에선 function과 mixin이 담당합니다. function은 숫자 계산용이고 mixin이 스타일링 문법을 묶는 용도입니다. 곁들여서 if와 for도 보여드리겠습니다.

### function
```scss
@function calculation($calculation-type, $var1, $var2) {
  @if $calculation-type == "plus" {
    @return $var1 + $var2;
  }
  @else if $calculation-type == "minus" {
    @return $var1 - $var2;
  }
  @else if $calculation-type == "time" { /* 곱하기 기호(*) 있는데 그냥 for문 보여드립니다. */
    $result: 0;
    @for $i from 0 to $var2 {
      $result: $result + $var1;
    }
    @return $result;
  }
  @else {
    @return $var1 / $var2;
  }
}
```
### mixin
```scss
@mixin example-7-rainbow($color, $size) {
  .example-7 .#{$color}-example {
    padding: $size;
    background-color: $color;
  }
}
```
⠀이걸 이용하면 위 테두리속성 예시가 더 개선될 겁니다. <span style='font-family:OngleipParkDahyeon'>개인적으로 조금 신기했던 게 저 위에 #{}입니다. 전 attribute를 변수명같이 생각중이었는데 변수값으로 변수명을 때워서 접근하다니... 다른 언어 쓰면서 하고 싶던 건데 이런 거 처음 봅니다. attribute가 변수명이 아니라 값같은 거였을까요? 모르겠네요.</span>

## 마무리
⠀CSS는 딱히 깊게 알 필요가 없다고 생각해서 이정도에서 끝내겠습니다. 이제 이론은 끝났고 다음 포스트부터는 Jekyll에 적용해 보겠습니다.