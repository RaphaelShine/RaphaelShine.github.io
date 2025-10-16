---
title: "[Blog]15. Jekyll의 HTML 파일 정리"
excerpt: "Jekyll의 HTML 파일들(includes, layouts)의 Minimal-Mistakes를 기준으로 구체적으로 정리하고 본 블로그에서 수정된 내용(포스트 이동버튼 카테고리 기준 수정 등)을 알아본다."

sort_key : 15
categories:
  - Blog
tags:
  - [Blog-구체적으로, MMistakes, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-16
last_modified_at: 2025-10-16

gallery:
  - url:
    image_path: /assets/images/TheEarthCapture.png
    alt: "사진 1"
  - url:
    image_path: /assets/images/TheEarthCapture.png
    alt: "사진 2"
  - url:
    image_path: /assets/images/TheEarthCapture.png
    alt: "사진 3"
  - url:
    image_path: /assets/images/TheEarthCapture.png
    alt: "사진 4"
  - url:
    image_path: /assets/images/TheEarthCapture.png
    alt: "사진 5"
  - url:
    image_path: /assets/images/TheEarthCapture.png
    alt: "사진 6"
---
## 시작하며
⠀사전처럼 쓰시면 되겠습니다.

⠀참고로 저는 Minimal-Mistakes를 fork해왔기 때문에 Minimal-Mistakes의 파일 기능과 그것을 어떻게 수정했는지를 중심으로 설명합니다. 이 템플릿을 쓰지 않았더라도 원하는 부분은 찾아서 가져가 쓰실 수 있습니다.

⠀블로그의 파일은 대부분이 HTML이라 이 포스트가 상당히 길어질 예정입니다. 알 필요 없는 부분은 넘어가겠습니다.

## **1. `index.html`**
⠀[홈 페이지](/)입니다. HTML이라 Markdown 못 쓰니 Markdown 문서에서 작성 후, 개발자도구로 HTML 복붙하는 것도 방법입니다.

## **2. `_includes/` 폴더**
⠀이 폴더에는 다른 파일에서 불러올 HTML 조각들을 담습니다. 포스트 목록 나열부터 포스트 날짜 표시나 다음/이전 포스트 이동 버튼까지, 다 여기 있습니다. Liquid로 다음과 같이 작성하면 조각이 불러와집니다.
```liquid
{% raw %}{% include filename.html parameter=value %}{% endraw %}
```
⠀parameter를 설정한다면 included file에서 `include.parameter`로 접근할 수 있습니다.
### `comments-providers/`, `comments.html`, `comment.html`
⠀댓글에 사용되는 조각입니다. 자세한 건 [댓글 만드는 포스트](/blog/blog-14-creating-comment-system/)에서 확인하십시오.
### `search/`
⠀사이트 내 검색 기능으로 선택할 수 있는 프로그램들이 담겨있습니다. 기본은 lunr입니다.
### `scripts.html`
⠀사이트 내 검색 기능과 분석기능에 대해 다루는 듯합니다. 잘은 모르겠습니다.

⠀내부 include: `analytics.html`, `/comments-providers/scripts.html`
### `archive-single.html`
⠀포스트 목록을 나열할 때, 각 포스트 하나를 나타냅니다.

⠀내부 include: `page__meta.html`
### `sidebar.html`
⠀왼쪽에 있는 바입니다.

⠀내부 include: `author-profile.html`, `nav_list`
### `author-profile.html`
⠀수정은 불필요합니다. 수정은 밑에 있는 파일에서 합니다.

⠀지금 왼쪽 바에 보이는 게 이 조각입니다. 아바타(이미지)부터 링크들까지 보여줍니다. `_config.yml`에서 설정한 author의 속성들을 가져오므로 `_config.yml`에만 값을 넣어주면 알아서 해 줍니다. 이미 만들어진 링크가 아닌 다른 링크를 넣고 싶다면 `_config.yml`에서 변수를 더 추가한 후, `author-profile-custom-links.html`에 코드를 넣습니다.
### `breadcrumbs.html`
⠀수정했습니다.

⠀문서마다 상단에 디렉토리 경로처럼 뜨는 부분입니다. 소환:
{% include breadcrumbs.html %}
⠀저는 카테고리를 묶는 field라는 범주를 하나 더 만들었기 때문에 breadcrumbs(빵가루라는 뜻)에 category와 field가 다 떠야 했습니다. 원래는 문서의 url을 잘라서 각각의 링크로 만드는 형식이어서 그냥 url을 baseurl/field/category/title로 만들면 됐겠지만 불필요한 정보를 주고 싶지 않았기 때문에 여기를 고쳤습니다. 대충 설명하자면, category를 알면 `site.data.navigation.yml`에서 field가 어딘지 알 수 있기 때문에 그걸 가져와서 억지로 끼워넣는 코드입니다. 저는 navigation에서 field와 category의 위계를 설정해 두었기 때문에 navigation을 중심으로 반복문을 돌리게 되었습니다.

### `page__taxonomy.html`
⠀밑의 두 파일을 가져와 \<head>부분에서 문서의 카테고리와 태그에 대한 메타정보를 알려줍니다.

⠀내부 include: `category-list.html`, `tag-list.html`
### `documents-collection.html`
⠀home이나 collection [layout](#_layouts)에서 문서 나열을 위해 사용합니다.
### `head.html`
⠀모든 문서의 \<head>에 들어갑니다. 수정 사항이 있으면 `_includes/head/custom.html`을 이용하십시오.
### `footer.html`
⠀모든 문서의 \<footer>에 들어갑니다. 소환 :
{% include footer.html %}
<br>
⠀수정 사항이 있으면 `_includes/footer/custom.html`을 이용하십시오.

{% include figure image_path="/assets/images/TheEarthCapture.png"
   alt="profile"
   caption="네모로 각진 땅을 가진 지구 사진<br> (라임~)"
   class="align-left"
   style="width:170px" %}
### `figure`
⠀수정했습니다.

⠀확장자는 없지만 HTML입니다. HTML의 \<figure>를 이용해 Markdown 문법 대신 이미지를 멋들어지게 뽑아줍니다. 왼편의 사진이 이 방식을 사용했습니다. 이 부분은 [다른 포스트](/blog/blog-13-uploading-Image/)에서 따로 자세히 설명하겠습니다.

⠀원래 style을 임의 지정할 수 없는데, 이를 임의 지정할 수 있도록 바꿨습니다. 빨간줄이 뜨긴 하는데 작동은 합니다. 살짝 위험할지도 모르겠습니다.

<br>

### `gallery`
⠀확장자는 없지만 HTML입니다. HTML의 \<figure>를 이용해 이미지셋을 멋들어지게 뽑아줍니다. 이 부분은 [다른 포스트](/blog/blog-13-uploading-Image/)에서 따로 자세히 설명하겠습니다.

{% include gallery %}
### `masthead.html`
⠀수정했습니다.

⠀상단의 navigation바를 만드는 조각입니다. 소환 :
{% include masthead.html %}
⠀원래는 navigation바는 별 다른 것 없이 제목과 버튼만 있었는데, 이를 수정해 마우스 hover 시 하위목록을 보여주도록 만들었습니다. 저 html만으로는 숨어있다가 나오지 못하므로 [CSS](/blog/blog-12-how-to-use-css/#상단바-세부목록)를 사용해야 합니다. 이 수정이 제가 처음 뜯어고치려고 한 부분이라 아직 미숙해서 여기는 ChatGPT의 도움을 받았습니다. 
### `page__date.html`
⠀수정했습니다.

⠀포스트 상단에 개시/수정 날짜 보여주는 조각입니다. 소환 :
{% include page__date.html %}
⠀한국식으로 표기되도록 바꾸고 아이콘도 바꿨습니다.
### `page__hero.html`
⠀수정했습니다.

⠀포스트 상단에 [제목 뒤쪽으로 이미지 까는](/blog/blog-11-how-to-use-yaml/#제목-뒤쪽에-이미지-띄우기) 조각입니다.

⠀`page__meta.html`를 include하던 걸 `page__date.html`로 바꾸고, [`single.html`](#singlehtml)에서 hero가 있을 때 `posts-taxonomy.html`를 띄우지 않는 걸 제대로 띄우도록 `single.html`도 고쳤습니다.
### `page__meta.html`
⠀수정했습니다.

⠀포스트 목록에서 각각의 포스트 정보를 보여줍니다. 소환 :
{% include page__meta.html %}
⠀개시 날짜와 수정 날짜가 같으면 개시 날짜만 보이도록 수정했습니다.
### `page__related.html`
⠀맨 밑에 연관 포스트로 뜨는 조각입니다.
⠀내부 include: `archive-single`, `before-related.html`
### paginator, -v1, -v2
⠀포스트 목록이 길어지면 다음 페이지로 자릅니다. 이걸 쓰는 포스트 목록 조각은 home layout밖에 없습니다.
### `post_pagination.html`
⠀수정했습니다.

⠀포스트 하단에서 다음/이전 포스트로 넘어가는 버튼 조각입니다. 소환 :
{% include post_pagination.html %}
### `posts-category.html`, `posts-tag.html`
⠀매개변수로 받은 카테고리나 태그의 포스트를 나열합니다.

⠀내부 include: `archive-single.html`
### `posts-taxonomy.html`
⠀수정했습니다.

⠀포스트 목록입니다. post들이 날짜순이 아니라 임의로 front matter에 만든 sort_key의 값을 기준으로 나열되도록 바꿨습니다.

⠀내부 include: `archive-single.html`
### `skip-links.html`
⠀tab키를 쓸 때 빠르게 이동할 수 있도록 돕는 조각입니다. 한국어로 되어있지 않으니 수정할 수 있습니다.
### `social-share.html`
⠀곧 수정 예정입니다.

⠀하단의 공유하기 조각입니다.
### `toc.html`
⠀오른쪽의 On This Page 조각입니다.
### `archive-category.html`
⠀제가 새로 만든 파일입니다.

⠀카테고리별로 포스트를 나열합니다.

## **3. `_layouts/` 폴더** 
⠀문서의 기본 틀들을 담습니다. front matter에 `layout: layoutname`을 쓰면 layoutname.html로 담아둔 파일을 기본 틀로 정합니다. layout 파일도 다른 layout을 따를 수 있습니다.

⠀content라는 변수는 해당 layout을 사용한 문서의 front matter를 제외한 본문 내용을 담습니다.

⠀layout 파일은 정말 중요한 몇개 정도만 소개하겠습니다.
### `default.html`
⠀layout의 layout까지 고려하면, 모든 문서가 이 문서의 틀 위에 있습니다. 가장 기본적인 틀입니다.

⠀내부 include: `head.html`, `head/custom.html`, `skip-links.html`, `masthead.html`, `after-content.html`, `search/search_form.html`, `footer.html`, `footer/custom.html`, `scripts.html`
### `archive.html`
⠀포스트를 제외한 페이지들은 거의 다 이 틀 위에 있습니다. 
### `single.html`
⠀모든 포스트가 이 문서의 틀 위에 있습니다. `_config.yml`에서 설정되어 있는 `site.defaults.values.layout`이 single로 되어있기 때문입니다. ([작은 수정](#page__herohtml))
### `field.html`
⠀제가 새로 만들었습니다. 저는 카테고리를 한 번 더 묶고 싶었기 때문에 카테고리 위의 field를 정의하고 같은 field인 카테고리를 나열하는 layout을 만들었습니다.