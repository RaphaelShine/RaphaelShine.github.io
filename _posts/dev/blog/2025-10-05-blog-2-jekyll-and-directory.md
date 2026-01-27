---
title: "[Blog]2. Jekyll의 디렉토리 구조 ( + Minimal-Mistakes )"
excerpt: "블로그를 만드는 프로그램 지킬(Jekyll)에 대해 배운 후, Jekyll, Minimal-Mistakes의 기본 폴더 구조를 정리한다."

sort_key : 2
categories:
  - Blog
tags:
  - [Blog-뼈대, MMistakes, Blog-날먹, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-05
last_modified_at: 2025-10-14
---

## 시작하며
⠀이 포스트에서는 먼저 Jekyll이 무엇인지 설명한 후, Jekyll의 디렉토리 구조를 Minimal-Mistakes에 초점을 맞춰 겉핥기로 알아보겠습니다. 구조의 상세한 내용은 계속되는 포스트에서 설명하겠습니다. (Jekyll 자체에 대한 설명은 좀 어려울 수 있으니 넘어가도 됩니다.)

## Jekyll에 대하여
⠀Github Pages는 Jekyll을 기본적으로 지원합니다. Jekyll은  Liquid와 Markdown을 해석해 HTML로 바꾸는 빌더의 일종으로, `_site` 폴더를 만들어 웹 사이트를 구동합니다. 내부적으로는 Ruby라는 언어를 사용합니다.

### 언더스코어 `_`
⠀파일 또는 폴더들의 이름을 보면 앞에 언더스코어`_`가 붙는 게 있고 안 붙는 게 있는데, 붙으면 대충 딴 코드에서 접근하겠다는 뜻, 안 붙으면 알아서 살겠다는 뜻입니다.

<details><summary>정확히는(어려운 소리니 넘어가도 됩니다.)</summary><div markdown="1">

⠀언더스코어 파일or폴더는 Jekyll이 렌더링하여 `site.data`나 `site.posts`처럼 접근하게 되고, 언더스코어가 아닌 파일은 Jekyll이 정적 파일로 저장해 `site.static_files`로 접근하게 됩니다. `site.static_files`에 들어있는 파일은 다음과 같은 속성을 갖습니다.

|속성|의미|
|:---:|:---|
| path | 파일 위치 e.g. /assets/img/image.png|
| modified_time | 마지막 수정시각(시각 타입)|
| name | 파일명|
| basename | 확장자 제외한 파일명|
| extname | 확장자명|

e.g.
```liquid
{% raw %}{% for nav_button in site.data.navigation.main %}
  {{ nav_button.title }}
{% endfor %}
{% for file in site.static_files %}
  {{ file.name }}
{% endfor %}{% endraw %}
```
결과 (웹사이트에서 직접 실행됨)
```
{% for nav_button in site.data.navigation.main %}{{ nav_button.title }}{% endfor %}
{% for file in site.static_files %}{{ file.name }}{% endfor %}
```
</div></details>

### front matter
⠀**front matter**는 HTML의 head와 비슷하게 문서의 메타 데이터를 저장하는 부분입니다.

⠀Jekyll은 파일이 `.yml` 또는 `.yaml`이 아니더라도 **front matter**를 갖고 있으면 **front matter** <span style='color:yellow'>내부 내용을 YAML로 처리</span>합니다. 또한 그 파일을 <span style='color:yellow'>빌드 대상으로 판단</span>하는 역할도 합니다. 따라서 front matter를 갖고 있거나 빌드 대상 파일이 include 또는 @import하지 않은 파일은 빌드를 거치지 않고 저장됩니다. front matter를 달아놓고 언더스코어를 두면 에러가 났던 것 같습니다.

⠀다음과 같이 `---` 두 개 사이는 frontmatter가 됩니다.
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

### Collections (어려운 소리니 넘어가도 됩니다.)
<details><div markdown="1">

⠀post들은 기본적으로 `_posts` 안에 저장되는데, post를 다른 폴더로도 묶을 수 있도록 Jekyll에서 **Collections**를 지원합니다. `_config.yml`에 다음과 같이 적으면 됩니다.
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
⠀development와 literature라는 Collection이 만들어졌습니다. output이 true면 permalink에 정의된 대로 아카이브 페이지를 빌드합니다. 정렬 기준은 `sort_by`에 대해 오름차순입니다. `sort_by`에는 해당 페이지를 나타내는 파일에서 front matter에 정의한 변수명을 넣으면 됩니다. `sort_by` 대신 `order`를 사용하면 하드코딩할 수 있습니다.

⠀Collection을 정의한 후, `_pages/`를 만든 것과 같이 Collection을 파일로 만들어야 합니다. `언더스코어+Collection이름`으로 이름을 짓습니다. 그리고 안에 해당 Collection에 포함하고 싶은 post를 넣습니다.

⠀`_config.yml`에서 collections_dir를 이용하면 Collection들을 한 폴더에 넣어줄 수 있습니다.
```yml
collections_dir : my_collections
```
⠀위와 같이 정의할 경우, Collection들을 묶는 폴더의 이름이 my_collections가 되어야 합니다. 참고로 `_posts/`도 Collection입니다. Jekyll에서 그렇게 하드코딩되어 있습니다. 따라서 폴더에 같이 넣어줍니다. `_pages/`도 Collection인지는 잘 모르겠습니다.

<span style='font-family:OngleipParkDahyeon'>⠀저는 이걸 알게 되기 전에 이미 post들을 나누는 체계를 만들어버렸기 때문에 조금 슬펐습니다. Collections를 이용했더라면 더 편했을지도 모르겠습니다. 그래서 저 대신 여러분들 쓰시라고 알려 드립니다.</span>
</div></details>

### drafts
⠀포스트를 다 쓰진 않아서 개시는 못하지만 저장은 하고싶은 경우: 초안으로 저장할 수 있습니다. `_drafts` 폴더를 만들어 안에 넣어두면 됩니다. 작명은 날짜 빼고 `title.md`로 합니다. 기본적으론 사이트에 보이지 않고 로컬 서버 실행 시 `jekyll serve --drafts`를 쓰면 초안을 볼 수 있습니다.

### page와 post에 대해 제공하는 속성들 (어려운 소리니 넘어가도 됩니다.)
<details><div markdown="1">

⠀post는 page와 다 똑같은데 포스팅 날짜 관련 속성이 더해진 형태입니다.

|:---:|:---|
|title|제목|
|excerpt|발췌 요약을 직접 작성 가능|
|excerpt_separator|본문에서 여기 넣은 문자가 나올 때까지를 발췌 요약으로 설정. 주석도 감지되기에 보통 `"<!--more-->"`를 사용.|
|categories|카테고리. `site.categories.카테고리이름`을 이용해 해당 카테고리를 가진 문서 리스트를 얻을 수 있습니다.|
|tags|태그. `site.tags.태그이름`을 이용해 위와 같습니다.|
|toc|true, false 오른쪽에 따라다니는 On This Page가 toc입니다.|
|toc_sticky|true, false 따라다닐지 결정합니다.|

post 속성

|:---:|:---|
|date|개시 날짜|
|last_modified_at|마지막 수정 날짜|

e.g. 이 포스트의 front matter

```markdown
---
title:  "[Blog]3. Jekyll의 구조"
excerpt: "Jekyll에 대해 배운 후, Jekyll, Minimal-Mistakes의 기본 폴더 구조를 정리한다."

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
```
</div></details>

### 기본적인 Jekyll의 디렉토리 구조
[Jekyll 공식사이트](https://jekyllrb.com/docs/structure/){:target="_blank" rel="noopener noreferrer"}에 이렇게 소개하고 있습니다.
```
.
├── _config.yml
├── _data
│   └── members.yml
├── _drafts
│   ├── begin-with-the-crazy-ideas.md
│   └── on-simplicity-in-technology.md
├── _includes
│   ├── footer.html
│   └── header.html
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
│   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
│   ├── _base.scss
│   └── _layout.scss
├── _site
├── .jekyll-cache
│   └── Jekyll
│       └── Cache
│           └── [...]
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid front matter
```

## Minimal-Mistakes의 구체적인 디렉토리 구조
템플릿이 다르더라도 상위 폴더들의 기능은 같습니다. 하위 파일은 무시하고 보면 됩니다.
### `_data/`
`_config.yml`이라는 특별한 파일이 아닌 다른 YAML 파일들을 담습니다. Minimal-Mistakes에선 `navigation.yml`과 `ui-text.yml`이 들어있습니다. [YAML 파일]

- `navigation.yml`는 네비게이션(상단바)의 정보를 저장합니다.

- `ui-text.yml`는 블로그 기본 단어를 언어별로 저장합니다.

### `_includes/`
주로 자주 쓰는 HTML을 Liquid에서 &#123;%include%&#125;를 써 꺼내오기 위해 사용합니다. [HTML 파일]

- `analytics-providers/`는 블로그의 통계값을 제공하는 provider의 코드를 가져옵니다. 어떤 provider를 쓸지는 `_config.yml`에서 정합니다.

- `comments-providers/`는 댓글 기능을 제공하는 provider의 코드를 가져옵니다. 어떤 provider를 쓸지는 똑같이 `_config.yml`에서 정합니다.

- `search/`는 검색기능을 제공하는 코드를 가져옵니다. 어떤 provider를 쓸지는 똑같이 `_config.yml`에서 정합니다.

- 여기 있는 파일은 liquid의 include를 사용해 다른 코드로 꺼내올 수 있습니다. 그러면 사이트에서 그 영역에 해당 HTML 조각이 들어갑니다.

### `_layouts/`
문서를 유형별로 기본적인 형태를 만들어 layout으로 이곳에 담습니다. 포스트나 페이지를 만들고 front matter에서 그 레이아웃을 선택할 수 있습니다. [HTML 파일]

### `_pages/`
여러분이 만든 페이지들을 담으시면 됩니다. [Markdown에 대하여]

### `_posts`
여러분이 만든 포스트들을 담으시면 됩니다. **포스트 제목은 항상 xxxx-xx-xx-title.md로 짓습니다.** 그래야 Jekyll이 정확히 인식해야 하기 때문입니다. [Markdown에 대하여]

### `_sass/`
CSS 파일들을 담습니다. 템플릿을 선택했다면 템플릿 파일이 거의 본체일 겁니다. 템플릿 파일인 `minimal-mistakes/` 안에는 `skins/`, `vendor/`가 있습니다. [CSS 파일]

- `skins/`는 `_config.yml`에서 지정할 수 있는 테마들이 저장됩니다.

- `minimal-mistakes/` 밑에 많은 `.scss`가 있는데, 이들은 사이트의 파츠별로 잘 나뉘어 있어서 그냥 수정하고 싶은 부분 찾아서 여기서 수정하면 되겠습니다.

- 그 많은 `.scss`중 `_variables.scss`는 직접 HTML 파츠에 대응하는 아이가 아니라 CSS에서 쓸 변수들을 담는 파일입니다.

### `assets/`
`main.scss`가 담겨있는 `css/` 폴더, `images/`, `js/`가 있습니다. [CSS 파일]

- `main.scss`는 언더바된 다른 `.scss`들을 @import해줍니다. CSS 함수가 어디있는지 몰라서 수정이 어려울 때 여기에다가 선언해주면 override 할 수 있는 것 같습니다.

### `_config.yml`
사이트의 기본 변수를 담습니다. 여러분이 수정하고 싶은 사이트 설정은 여기서 변수를 수정하면 적용됩니다. [YAML 파일]

### `index.html`
퍼마링크 없는 순수한 사이트주소에서 뜨는 화면입니다.

### `_site/`
Jekyll이 만들어내는 정적 사이트의 본체입니다. 여러분이 코드를 push하면 Jekyll이 만드는 것이니 여러분께는 없을 겁니다. 플러그인에서 여기에 사이트맵을 담아줍니다. 플러그인을 사용하지 않고 직접 담도록 코드를 짤 수도 있긴 합니다.

## 마무리
⠀진짜 이걸 내가 하루아침에 다 배운 거라니 뇌가 참 말랑말랑해진 기분입니다.

⠀이제 좀 익숙해져서 이젠 따로 다른 블로그를 찾아보진 않습니다. [Jekyll 공식사이트](https://jekyllrb.com/){:target="_blank" rel="noopener noreferrer"}의 내용과 수많은 에러메시지에게 배웠습니다.

⠀이후 포스트들은 먼저 초보용과 고수용으로 나누어 이론을 설명한 후 구체적으로 Jekyll에서 어떻게 쓰이는지를 알아볼 것입니다. 이론을 이미 알고 있거나 너무 어렵다면 바로 Jekyll 파일에서의 쓰임 포스트로 넘어가시면 됩니다.

⠀여러분은 열정!을 챙기고 시작하신 분들이니 포기 마시고 열심히 해 봅시다.

||초보용|고수용|활용|
|:---|:---|:---|:---|
|HTML|[이동](/blog/blog-3-newbie-html/)|[이동](/blog/blog-7-hard-html-and-liquid/)|[이동](/blog/blog-10-how-to-use-html/)|
|Markdown|[이동](/blog/blog-4-newbie-markdown/)|[이동](/blog/blog-8-hard-markdown/)|여러분이 처음부터 쓰는 거라 없음|
|YAML|[이동](/blog/blog-4-newbie-markdown/)|쉬워서 없음|[이동](/blog/blog-11-how-to-use-yaml/)|
|CSS|[이동](/blog/blog-6-newbie-css/)|[이동](/blog/blog-9-hard-css/)|[이동](/blog/blog-12-how-to-use-css/)|

[HTML 파일]:/blog/blog-15-html-files/
[Markdown에 대하여]:blog/blog-4-newbie-markdown/
[CSS 파일]:blog/blog-17-css-files/
[YAML 파일]:blog/blog-16-yaml-files/