---
title: "[Blog]12. Jekyll의 CSS 활용, 파일 정리"
excerpt: "블로그에서 원하는 글꼴(폰트) 설정, 글자 크기 설정, 부가적인 CSS 탑재 방법을 배운다. Jekyll에서 구체적인 CSS 파일들을 Minimal-Mistakes 기준으로 정리한다."

sort_key : 12
categories:
  - Blog
tags:
  - [Blog-구체적으로, MMistakes, Blog-날먹, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-11
last_modified_at: 2025-10-14
---

## 시작하며
⠀CSS를 이용하면 원하는 폰트를 설정하고 어떤 요소든 사이즈를 조절할 수 있습니다. 그 방법들을 알려드린 뒤에 파일들을 정리해 둘 테니 사전처럼 쓰시면 되겠습니다. CSS 파일들은 `assets/css/`에 있는 `main.scss`과 `_sass/`에 있는 세부 파일들이 있습니다.

⠀CSS 문법에 대해 이해가 필요하다면 [초보용](/blog/blog-6-newbie-css/)과 [고수용](/blog/blog-9-hard-css)이 준비되어 있습니다. 몰라도 그냥 따라만 하면 됩니다.
## 활용법
### 폰트 설정하기
⠀먼저 인터넷에서 웹 폰트를 url로 얻어 옵니다. 저는 [누누](https://noonnu.cc/index){:target='_blank' rel='noopener noreferrer'}에서 가져왔습니다.

(웹폰트로 사용 사진)

⠀웹폰트로 사용으로 복사해 텍스트를 [`assets/css/main.scss`](#mainscss)에 넣습니다.

⠀[`minimal-mistakes/_variables.scss`](#minimal-mistakes_variablesscss)에서 `/* system typefaces */`를 찾아 각 font-family 값을 넣습니다. serif는 좀 진지해 보이는 폰트(획 끝이 돌출된 글꼴)고 sans-serif와 sans-serif-narrow는 둥근 폰트, monospace는 코딩용 폰트입니다. <span style='font-family:OngleipParkDahyeon'>저는 귀여운 글꼴 넣는 블로그를 보고 감명받아서 cutie라는 새 변수를 만들었습니다.</span> 저장하면 끝입니다.

```scss
/* system typefaces */
$serif: 'BookkMyungjo' !default;
$sans-serif: 'NanumSquareRound' !default;
$sans-serif-narrow: 'NanumSquareRound' !default;
$monospace: 'D2Coding' !default;
$cutie: 'OngleipParkDahyeon' !default;
```

### 글자 크기 변경하기
⠀저는 [파일을 하나](#_fontsizescss) 새로 만들었습니다. 가져가서 `_sass/` 밑에 넣으십시오. `.page__content`가 본문 글자 선택자이니 여기 달린 `set-font-size()`의 $size 값만 조절하면 본문 글자 크기가 변합니다. 다른 특정 요소를 대상으로 하고 싶다면 그 아래에서 또 해당 선택자 불러서 `set-font-size()` 붙여주면 됩니다. 저는 보이는 바와 같이 인라인 코드 크기도 수정했습니다.

### 색상 변경하기
⠀군말 없이 템플릿 그대로 쓸 수도 있겠지만, 바꾸고 싶은 색이 보인다면 `_sass/skins/`에서 여러분이 택한 skin의 파일로 가서 찾거나 `_sass/variables.scss`에서 찾으면 됩니다. `mix()`라는 걸 쓰기도 하는데, 어렵지 않습니다. 그냥 두 색을 몇 퍼센트 피율로 섞어 만들겠다는 겁니다.

```scss
$code-background-color: mix(#000, $background-color, 15%) !default; //원본

$code-background-color: mix(#000, $background-color, 70%) !default; //수정
```

### 링크 텍스트 밑줄 없애기
⠀원래 댓글 기능 만드는 게 막막해서 여기저기 찾다가 [이 블로그](https://devinlife.com/howto%20github%20pages/github-pages-settings/)에서 엄청 좋은 걸 새로 얻게 되었습니다. 원래 <u><a>이렇게</a></u> 되는 걸 <a>이렇게</a> 만들어 줄 수 있습니다. `_sass/minimal-mistakes/_base.scss`에서 이렇게 하면 됩니다.
```scss
/* links */

a {
  /* devinlife : a link 하이퍼링크 밑줄 없애기 */
  text-decoration: none;

  &:focus {
    @extend %tab-focus;
  }

  &:visited {
    color: $link-color-visited;
  }

  &:hover {
    color: $link-color-hover;
    outline: 0;
  }
}
```

## Jekyll 디렉토리의 파일들
⠀참고로 저는 Minimal-Mistakes를 fork해왔기 때문에 Minimal-Mistakes의 파일 기능과 그것을 어떻게 수정했는지를 중심으로 설명합니다. 이 템플릿을 쓰지 않았더라도 원하는 부분은 찾아서 가져가 쓰실 수 있습니다.
### `main.scss`
⠀이 파일만이 front matter를 가지고 다른 파일들을 @import 합니다. 새 파일을 만들면 여기서 @import해야 합니다. Directory 구조는 `assets/css/main.scss`입니다.

⠀저는 **폰트 설정**과 본문 너비 제한 제거, sidebar 너비 수정을 위해 수정했습니다. 정확히 어디를 고쳐야 할지 모르겠을 때, 여기에서 수정하면 override 됩니다.

<details><div markdown="1">

```scss
//기본 minimal-mistakes
@charset "utf-8";
@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin | default: 'default' }}"; // skin
@import "minimal-mistakes"; // main partials

//custom
@import "fontsize";
@import "navigationhover";

//너비 설정
$max-width: 100vw;  // 본문 너비 무제한
$right-sidebar-width-narrow: 200px;  // large일 때 sidebar 너비
$right-sidebar-width:        220px;  // x-large일 때 sidebar 너비

//폰트 설정
@font-face {
    font-family: 'D2Coding';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_three@1.0/D2Coding.woff') format('woff');
    font-weight: normal;
    font-display: swap;
}
@font-face {
    font-family: 'NanumSquareRound';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_two@1.0/NanumSquareRound.woff') format('woff');
    font-weight: normal;
    font-display: swap;
}
@font-face {
    font-family: 'BookkMyungjo';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2302@1.0/BookkMyungjo-Lt.woff2') format('woff2');
    font-weight: 400;
    font-display: swap;
}
@font-face {
    font-family: 'OngleipParkDahyeon';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/2411-3@1.0/Ownglyph_ParkDaHyun.woff2') format('woff2');
    font-weight: normal;
    font-display: swap;
}
```

</div></details>

### `minimal-mistakes/_variables.scss`
⠀CSS 파일에서 쓰이는 변수들을 모은 파일입니다. 여기서 변수 쇼핑하거나 수정하면 됩니다. 밑에 둔 것들은 아주 중요한 것들. 이 외에도 여러 색상 변수들이 정의되어 있습니다.

<details><div markdown="1">

```scss
// 문서의 기준 사이즈
$doc-font-size: 16px !default;
$doc-font-size-medium: $doc-font-size * 1.125 !default;
$doc-font-size-large: $doc-font-size * 1.25 !default;
$doc-font-size-x-large: $doc-font-size * 1.375 !default;

// 폰트 설정
/* system typefaces */
$serif: 'BookkMyungjo' !default;
$sans-serif: 'NanumSquareRound' !default;
$sans-serif-narrow: 'NanumSquareRound' !default;
$monospace: 'D2Coding' !default;
$cutie: 'OngleipParkDahyeon' !default;

$global-font-family: $sans-serif !default;
$header-font-family: $sans-serif !default;
$caption-font-family: $serif !default;

// 폰트 크기
/* type scale */
$type-size-1: 2.441em !default; // ~39.056px
$type-size-2: 1.953em !default; // ~31.248px
$type-size-3: 1.563em !default; // ~25.008px
$type-size-4: 1.25em !default; // ~20px
$type-size-5: 1em !default; // ~16px
$type-size-6: 0.75em !default; // ~12px
$type-size-7: 0.6875em !default; // ~11px
$type-size-8: 0.625em !default; // ~10px

/* headline scale */
$h-size-1: 1.563em !default; // ~25.008px
$h-size-2: 1.25em !default; // ~20px
$h-size-3: 1.125em !default; // ~18px
$h-size-4: 1.0625em !default; // ~17px
$h-size-5: 1.03125em !default; // ~16.5px
$h-size-6: 1em !default; // ~16px
```

</div></details>

### `_fontsize.scss`
⠀제가 직접 만들었습니다. 글씨 크기를 조절하는 파일입니다. 파일 경로는 `_sass/_fontsize.szss`입니다. `breakpoint()`는 화면 크기에 따라 폰트 사이즈를 바꾸는 역할을 합니다. 우선순위가 높아서 폰트 크기 바꾼다고 다른 곳에서 열심히 깨작거려봐도 무시당합니다. 이 아이를 써야 합니다.

<details><div markdown="1">

```scss
//글씨 크기 조절
@mixin set-font-size($size) {
    @include breakpoint($small) {
      font-size: $size * 0.6 !important;
    }
    @include breakpoint($medium-wide) {
      font-size: $size * 0.7 !important;
    }
    @include breakpoint($medium) {
      font-size: $size * 0.8 !important;
    }
    @include breakpoint($large) {
      font-size: $size * 0.9 !important;
    }
    @include breakpoint($x-large) {
      font-size: $size !important;
    }
    @include breakpoint($max-width) {
      font-size: $size !important;
    }
}

//인라인코드
code.language-plaintext.highlighter-rouge {
  @include set-font-size(1em);
}
//본문 
.page__content {
    @include set-font-size(0.8em);
}

```

</div></details>

### `navigationhover.scss`
⠀ChatGPT가 짠 코드입니다. 본 블로그처럼 상단 바에서 목록이 나오도록 하고 싶다면 가져가십시오. *HTML과 YAML도 같이 맞춰줘야 합니다.*

<details><div markdown="1">

```scss
/* 1) hover 브리지 제거: 부모 클릭/hover 가로채지 않게 */
#site-nav li > .sub-menu::before {
  content: none !important;
}

/* 2) 부모 앵커를 위 레이어로 (애니메이션 중 겹쳐도 클릭 보장) */
#site-nav li.masthead__menu-item > a {
  position: relative;
  z-index: 2;
}

/* 3) 모든 1뎁스 메뉴 li를 절대배치 기준점으로 고정 */
#site-nav .visible-links > li,
#site-nav .hidden-links  > li,
#site-nav li.masthead__menu-item {
  position: relative !important;
}

/* 4) 서브메뉴 박스: 부모 아래 중앙 정렬 + 기본은 숨김 */
#site-nav li > .sub-menu {
  display: flex !important;      /* 세로 스택 + gap 사용 */
  flex-direction: column;
  gap: 10px;                     /* ← 항목 사이 간격(여기 숫자만 바꾸면 됨) */
  position: absolute;
  top: 100%;                     /* 부모 바로 아래에 밀착 */
  left: 50%;                     /* 가로 중앙 기준 */
  transform: translate(-50%, -14px);  /* 초기 상태: 살짝 위에서 시작(애니메이션용) */

  min-width: 180px;
  margin: 0;
  padding: 12px;                 /* 박스 안쪽 여백 */
  list-style: none;

  background: #252a34;           /* 네가 쓰던 배경 유지 */
  border: 1px solid #ddd;
  box-shadow: 0 6px 20px rgba(0,0,0,.08);
  z-index: 1;

  opacity: 0;
  visibility: hidden;
  pointer-events: none;
  transition: opacity .18s ease, transform .18s ease, visibility 0s linear .18s;
}

/* 5) 열릴 때: 부모 hover/포커스 OR 서브메뉴 자체 hover 모두 허용 */
#site-nav li:hover > .sub-menu,
#site-nav li:focus-within > .sub-menu,
#site-nav li > .sub-menu:hover {
  opacity: 1;
  visibility: visible;
  transform: translate(-50%, 0);   /* 위에서 아래로 스르륵 */
  pointer-events: auto;
  transition: opacity .18s ease, transform .18s ease;
}

/* 6) 서브메뉴 항목(링크) 스타일: 가운데 정렬 + 히트영역 */
#site-nav li > .sub-menu a {
  display: block;
  text-align: center;              /* 글자 가운데 정렬 */
  padding: 8px 12px;               /* 항목 자체의 클릭 영역(원하면 키워도 됨) */
  border-radius: 6px;              /* hover 배경 모서리 */
  text-decoration: none;
  color: inherit;
}

#site-nav li > .sub-menu a:hover,
#site-nav li > .sub-menu a:focus {
  background: #2f3542;             /* 호버 배경(원하면 조정) */
}

/* 7) 잘림 방지 */
.masthead, .masthead__inner-wrap, .masthead__menu,
.greedy-nav, .greedy-nav .visible-links, .greedy-nav .hidden-links {
  overflow: visible !important;
}

/* 8) flex-gap 폴백: 아주 구형 브라우저에서 gap 미지원 시 */
@supports not (gap: 1px) {
  #site-nav li > .sub-menu { display: block !important; }
  #site-nav li > .sub-menu li + li { margin-top: 10px; } /* 항목 간 간격 */
}


/* 부모 메뉴 버튼 크기 키우기 + hover 히트영역 확대 */
.greedy-nav .visible-links > li.masthead__menu-item > a {
  /* 간격은 작게, 버튼 자체는 크게 */
  margin: 0 .25rem;          /* 기본은 0 1rem 이라 간격이 큼 → 줄여서 '버튼 크기' 위주로 */
  padding: .65rem 1.1rem;    /* ↑ 세로/가로 패딩 늘려 클릭(hover) 영역 확대 */
  border-radius: .5rem;      /* 버튼 느낌 */
  line-height: 1;            /* 폰트 내부 여백 영향 최소화 */
}
/* hover시 버튼 배경 강조(필요하면 색만 조정) */
.greedy-nav .visible-links > li.masthead__menu-item > a:hover,
.greedy-nav .visible-links > li.masthead__menu-item:hover > a {
  background: mix($background-color, $primary-color, 92%);
  border-radius: .5rem;
}

/* 기본 테마의 밑줄 애니메이션이 버튼 배경과 겹치면 살짝 두껍게/유지하고 싶으면 이대로 둠 */
.greedy-nav .visible-links > li.masthead__menu-item > a::before {
  height: 4px;   /* 필요 시 6px 등으로 */
  bottom: 0;
}

/* 드롭다운 있는 부모도 동일 버튼 크기 유지 */
.greedy-nav .visible-links > li.masthead__menu-item.has-children > a {
  padding-right: 1.25rem; /* 화살표/아이콘 여유 */
}
```

</div></details>
