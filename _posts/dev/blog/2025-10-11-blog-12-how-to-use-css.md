---
title: "[Blog]12. Jekyll에서 폰트, 글자 크기, 색상 등 설정"
excerpt: "블로그에서 원하는 글꼴(폰트) 설정, 글자 크기 설정, 부가적인 CSS 탑재 방법을 배운다."

sort_key : 12
categories:
  - Blog
tags:
  - [Blog-팁, MMistakes, Blog-날먹, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-11
last_modified_at: 2026-01-27
---

## 시작하며
⠀CSS를 이용하면 원하는 폰트를 설정하고 어떤 요소든 사이즈를 조절할 수 있습니다.

⠀CSS 문법에 대해 이해가 필요하다면 [초보용](/blog/blog-6-newbie-css/)과 [고수용](/blog/blog-9-hard-css)이 준비되어 있습니다. 몰라도 그냥 따라만 하면 됩니다.
## 폰트 설정하기
⠀먼저 인터넷에서 웹 폰트를 url로 얻어 옵니다. 저는 [눈누](https://noonnu.cc/index){:target='_blank' rel='noopener noreferrer'}에서 가져왔습니다.

(웹폰트로 사용 사진)

⠀웹폰트로 사용으로 복사해 텍스트를 [`assets/css/main.scss`](/blog/blog-17-css-files/#mainscss)에 넣습니다.

⠀[`minimal-mistakes/_variables.scss`](/blog/blog-17-css-files/#minimal-mistakes_variablesscss)에서 `/* system typefaces */`를 찾아 각 font-family 값을 넣습니다. serif는 좀 진지해 보이는 폰트(획 끝이 돌출된 글꼴)고 sans-serif와 sans-serif-narrow는 둥근 폰트, monospace는 코딩용 폰트입니다. <span style='font-family:OngleipParkDahyeon'>저는 귀여운 글꼴 넣는 블로그를 보고 감명받아서 cutie라는 새 변수를 만들었습니다.</span> 저장하면 끝입니다.

⠀<span style='font-family:NanumMyeongjoOldHangeul'>옛한글 표시되는 명조</span>
[나눔명조옛한글](https://noonnu.cc/font_page/1649){:target='_blank' rel='noopener noreferrer'}

```scss
/* system typefaces */
$serif: 'BookkMyungjo' !default;
$sans-serif: 'NanumSquareRound' !default;
$sans-serif-narrow: 'NanumSquareRound' !default;
$monospace: 'D2Coding' !default;
$cutie: 'OngleipParkDahyeon' !default;
```

## 글자 크기 변경하기
⠀저는 [파일을 하나](/blog/blog-17-css-files/#_fontsizescss) 새로 만들었습니다. 가져가서 `_sass/` 밑에 넣으십시오. `main.scss`에서 @import 해주는 것도 잊지 마십시오. `.page__content`가 본문 글자 선택자이니 여기 달린 `set-font-size()`의 $size 값만 조절하면 본문 글자 크기가 변합니다. 다른 특정 요소를 대상으로 하고 싶다면 그 아래에서 또 해당 선택자 불러서 `set-font-size()` 붙여주면 됩니다. 저는 보이는 바와 같이 인라인 코드 크기도 수정했습니다.

## 색상 변경하기
⠀군말 없이 템플릿 그대로 쓸 수도 있겠지만, 바꾸고 싶은 색이 보인다면 `_sass/skins/`에서 여러분이 택한 skin의 파일로 가서 찾거나 `_sass/variables.scss`에서 변수를 찾으면 됩니다. `mix()`라는 걸 쓰기도 하는데, 어렵지 않습니다. 그냥 두 색을 몇 퍼센트 피율로 섞어 만들겠다는 겁니다.

```scss
$code-background-color: mix(#000, $background-color, 15%) !default; //원본

$code-background-color: mix(#000, $background-color, 70%) !default; //수정
```

## 링크 텍스트 밑줄 없애기
⠀원래 댓글 기능 만드는 게 막막해서 여기저기 찾다가 [이 블로그(dev in life)](https://devinlife.com/howto%20github%20pages/github-pages-settings/)에서 엄청 좋은 걸 새로 얻게 되었습니다. 원래 <u><a>이렇게</a></u> 되는 걸 <a>이렇게</a> 만들어 줄 수 있습니다. `_sass/minimal-mistakes/_base.scss`에서 이렇게 하면 됩니다.
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
## 상단바 세부목록
⠀본 블로그에서 상단바에 마우스를 올리면 세부 목록이 나오는 것을 따라하고 싶다면 [CSS 코드](/blog/blog-17-css-files/#navigationhoverscss)와 [HTML 코드](/blog/blog-15-html-files/#mastheadhtml)를 가져가면 됩니다. 저 바는 HTML코드상 [`_data/navigation.yml`의 `main` 객체](/blog/blog-16-yaml-files/#_data)에 담긴 항목을 나열합니다.