---
title:  "[Blog]3. Jekyll의 구조 ( + Minimal Mistakes )"
excerpt: "Jekyll에 대해 배운 후, Minimal Mistakes의 기본 폴더 구조를 정리한다."

sort_key : 0103
categories:
  - Blog
tags:
  - [Blog-뼈대부터, Blog-초보, MMistakes]

toc: true
toc_sticky: true
 
date: 2025-10-05
last_modified_at: 2025-10-05
---

## 시작하며
⠀이 포스트에서는 먼저 Jekyll이 무엇인지 설명한 후, Minimal Mistakes의 파일의 구조를 겉핥기로 알아보겠습니다. 구조의 상세한 내용은 계속되는 포스트에서 설명하겠습니다. 오늘의 내용을 이해하는 데는 파일이 무엇인지만 알면 충분하리라 생각합니다. (Jekyll은 좀 어려울 수 있으니 넘어가도 됩니다.)

## Jekyll에 대하여
⠀Github Pages는 Jekyll을 기본적으로 지원합니다. Jekyll은  Liquid와 Markdown을 해석해 HTML로 바꾸는 빌더의 일종으로, _site` 폴더를 만들어 웹 사이트를 구동합니다. 내부적으로는 Ruby라는 언어를 사용합니다.

### 언더스코어 `_`
⠀파일 또는 폴더들의 이름을 보면 앞에 언더스코어`_`가 붙는 게 있고 안 붙는 게 있는데, 붙으면 대충 딴 코드에서 접근하겠다는 뜻, 안 붙으면 알아서 살겠다는 뜻입니다.

⠀정확히는, 언더스코어 파일or폴더는 Jekyll이 렌더링하여 site.data나 site.posts처럼 접근하게 되고, 언더스코어가 아닌 파일or폴더는 Jekyll이 정적 파일로 저장해 site.static_files로 접근하게 됩니다. site.static_files에 들어있는 파일은 다음과 같은 속성을 갖습니다.

|속성|의미|
|:---:|:---|
| path | 파일 위치 e.g. /assets/img/image.png|
| modified_time | 마지막 수정시각(시각 타입)|
| name | 파일명|
| basename | 확장자 제외한 파일명|
| extname | 확장자명|

e.g.
```liquid
{% for nav_button in site.data.navigation.main %}
  {{ nav_button }}
{% endfor %}
```

### front matter
⠀Jekyll은 파일이 `.yml` 또는 `.yaml`이 아니더라도 front matter를 갖고 있으면 front matter 내부 내용을 YAML로 처리합니다. 또한 그 파일을 빌드 대상으로 판단하는 역할도 합니다. 따라서 front matter를 갖고 있거나 빌드 대상 파일이 import하지 않은 파일은 빌드를 거치지 않고 저장됩니다. front matter를 달아놓고 언더스코어를 두면 에러가 났던 것 같습니다.

⠀다음과 같이 --- 두 개 사이는 frontmatter가 됩니다.
```markdown
---
# 여기가 front matter
title: "제목"
layout: single
permalink: /title/
---
<!--여기부터 본문입니다.-->
하하호호  
여러분 화이팅!!
```

### Collections
⠀post들은 기본적으로 `_posts` 안에 저장되는데, post를 다른 폴더로도 묶을 수 있도록 Jekyll에서 Collections를 지원합니다. `_config.yml`에 다음과 같이 적으면 됩니다.
```yml
collections :
  development :
    output : true
    permalink : /development/:name/
    sort_by : chapter
  literature :
    output : true
    permalink : /literature/:name/
    order : 
      - korean-poem.md
      - english-poem.md
      - poem-theory.md
```
⠀development와 literature라는 Collection이 만들어졌습니다. output이 true면 permalink에 정의된 대로 아카이브 페이지를 빌드합니다. 정렬 기준은 sort_by에 대해 오름차순입니다. sort_by에는 해당 페이지를 나타내는 파일에서 front matter에 정의한 변수명을 넣으면 됩니다. sort_by 대신 order를 사용하면 하드코딩할 수 있습니다.

⠀Collection을 정의한 후,  _pages/를 만든 것과 같이 Collection을 파일로 만들어야 합니다. 언더스코어+Collection이름으로 이름을 짓습니다. 그리고 안에 해당 Collection에 포함하고 싶은 post를 넣습니다.

⠀_config.yml에서 collections_dir를 이용하면 Collection들을 한 폴더에 넣어줄 수 있습니다.
```yml
collections_dir : my_collections
```
⠀위와 같이 정의할 경우, Collection들을 묶는 폴더의 이름이 my_collections가 되어야 합니다. 참고로 _posts/도 Collection입니다. Jekyll에서 그렇게 하드코딩되어 있습니다. 따라서 폴더에 같이 넣어줍니다. 예상인데 _pages/도 아마 Collection 아닐까 합니다.

⠀저는 이걸 알게 되기 전에 이미 post들을 나누는 체계를 만들어버렸기 때문에 조금 슬펐습니다. 제 코드는 살짝 하드코딩이 필요한데, Collections를 이용했더라면 더 편했을지도 모르겠습니다. 이 post를 쓰면서 조금 사용해 봤지만 이걸 지금 바꾸는 건 비효율적이라 생각되어 여러분께만 알려 드립니다.

### page와 post에 대해 제공하는 속성들
이건 나중에 할래......

## Minimal-Mistakes의 폴더 구조

### `_data/`
`navigation.yml`과 `ui-text.yml`이 들어있습니다. [YAML에 대하여]()

- `navigation.yml`는 네비게이션(상단바)의 정보를 저장합니다.

- `ui-text.yml`는 블로그 기본 단어를 언어별로 저장합니다.

### `_includes/`
주로 자주 쓰는 HTML을 꺼내오기 위해 사용합니다.  
`analytics-providers/`, `comments-providers/`, `search/`와 같은 외계어파일, 여러 HTML, `copyright.js`가 있습니다. [HTML에 대하여]()

- `analytics-providers/`는 블로그의 통계값을 제공하는 provider의 코드를 가져옵니다. 어떤 provider를 쓸지는 `_config.yml`에서 정합니다.

- `comments-providers/`는 이제 저도 배울 예정

- `search/`는 검색기능을 제공하는 코드를 가져옵니다.

- 여러분이 가장 많이 쓸 것은 수많은 HTML들입니다. 여기 있는 파일은 liquid의 include를 사용해 다른 코드로 꺼내올 수 있습니다. 그러면 사이트에서 그 영역에 해당 HTML이 들어갑니다.

- `copyright.js` : 저작권은 지키는 게 좋을 겁니다.

### `_layouts/`
여러 HTML이 담겨 있습니다. 포스트나 페이지를 만들면 그 레이아웃을 정할 수 있습니다. [HTML에 대하여]() 

### `_pages/`
여러분이 만든 페이지들을 담으시면 됩니다. 파일이 많아지면 안에 폴더를 또 만들어서 세부화 시켜도 됩니다. [Markdown에 대하여]()

### `_posts`
여러분이 만든 포스트들을 담으시면 됩니다. **포스트 제목은 항상 xxxx-xx-xx-title.md로 짓습니다.** 그래야 Jekyll이 정확히 인식해야 하기 때문입니다. [Markdown에 대하여]()

### `_sass/`
`minimal-mistakes/`가 거의 본체입니다. 그 안에는 `skins/`, `vendor/`가 있습니다. [CSS에 대하여]()

- `skins/`는 `_config.yml`에서 지정할 수 있는 테마들이 저장됩니다.

- `vendor/`는 저도 잘 모릅니다. `breakpoint/`라는 폴더가 있는데, CSS의 breakpoint를 선언하는 것 같습니다. 열심히 부딪혀 보니 알게된 사실: breakpoint가 화면의 크기를 받아서 사이트의 폰트 크기를 조절합니다. 이게 다른 폰트크기선언보다 중요도가 높아서 저는 여기서 조절해야 해야 했습니다. 다른 기능도 있겠지만 아직 모르겠습니다.

- `minimal-mistakes/` 바로 밑에 있는 많은 `.scss`가 있는데, 이들은 사이트의 파츠별로 잘 나뉘어 있어서 그냥 수정하고 싶은 부분 찾아서 여기서 수정하면 되겠습니다.

- 그 많은 `.scss`중 `_variables.scss`는 직접 HTML 파츠에 대응하는 아이가 아니라 CSS에서 쓸 변수들을 담는 파일입니다.

### `assets/`
`main.scss`가 담겨있는 `css/` 폴더, `images/`, `js/`가 있습니다. [CSS에 대하여]()

- `main.scss`는 언더바된 다른 `.scss`들을 @import해줍니다. CSS 함수가 어디있는지 몰라서 수정이 어려울 때 여기에다가 선언해주면 override 할 수 있는 것 같습니다.

### `_config.yml`
사이트의 기본 변수를 담습니다. 여러분이 수정하고 싶은 사이트 설정은 여기서 변수를 수정하면 적용됩니다. [YAML에 대하여]()

### 기타 파일들
이 중 `index.html`은 퍼마링크 없는 순수한 사이트주소에서 뜨는 화면입니다. 나머지는 딱히 알 필요 없을 듯합니다.

## 마무리
⠀진짜 이걸 내가 하루아침에 다 배운 거라니 뇌가 참 말랑말랑해진 기분입니다. 이렇게 수능공부를 해야 하는데......(중졸티 내기) 뭐 수능은 사실 이런 거 배우듯 공부하는 게 아니니까요. 그냥 열심히 살아야죠.

⠀이제 좀 익숙해져서 따로 블로그를 찾아보진 않았습니다. [Jekyll 공식사이트]()의 내용과 수많은 에러메시지에게 배웠습니다.

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>