---
title: "[Blog]8. 고수용 Markdown(Kramdown) 설명"
excerpt: "Markdown(마크다운)이 어떻게 HTML로 실현되는지 알아보며 더 다양한 문법을 배운다."

sort_key : 8
categories:
  - Blog
tags:
  - [Blog-뼈대, 프런트엔드, Blog-고수]

header:
  overlay_image: https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Markdown-mark.svg/2560px-Markdown-mark.svg.png
  overlay_filter: 0.3
  caption: "Markdown logo"

toc: true
toc_sticky: true

date: 2025-10-08
last_modified_at: 2025-10-14
---
## 시작하며
⠀Markdown은 HTML을 쉽게 쓰기 위한 텍스트 양식입니다. 지금 이 포스트를 포함하여, 블로그의 구체적인 모든 문서에 쓰입니다. HTML은 tag붙이고 attribute넣고 하는 수고로움이 많지만 Markdown은 이 중 상당수를 쓰기 쉬운 기호로 대체합니다. 전부는 대체하지 못하므로 글을 이 이상으로 자유롭게 쓰고 싶다면 HTML을 배워야 합니다. `.md`확장자를 사용하며, Markdown 파일에서도 HTML을 직접 쓸 수 있고 따라서 Liquid도 작동합니다. <span style='font-family:OngleipParkDahyeon'>Liquid는 우선순위도 커서 Markdown의 코드블럭으로 봉인할 수 없습니다. 그래서 Liquid 문법 설명할 때 힘들어요ㅠㅠ</span> 또, 해석 방법이 다양해서 조금 들쭉날쭉 할 수 있습니다.

⠀Kramdown은 Markdown의 상위호환으로, Markdown에 여러 기능이 더해집니다. 사실 정확히 이 포스트가 설명하는 것은 Kramdown 문법입니다. 근데 Markdown이란 이름이 너무 유명하니까 그냥 Markdown이라고 합시다. Jekyll은 Kramdown을 사용하기 때문에 우리는 그냥 Markdown이라고 부르면서 Kramdown을 쓰면 됩니다. <span style='font-family:OngleipParkDahyeon'>작명을 어떻게 했는지 바로 보이죠? 그냥 m a r k 뒤집어서 k r a m...</span>

⠀Markdown의 들쭉날쭉은 생각보다 더 강해서, `_config.yml`의 kramdown.input을 무엇으로 선택했는지에 따라 또 다릅니다. Minimal-Mistakes는 GFM을 사용하는데, Kramdown의 기능 일부가 막혀 있습니다. 모든 기능을 사용하려면 `input: Kramdown`으로 바꿔줘야 합니다. 제가 이걸 알게 되었을 때는 설정을 Kramdown으로 바꿨더니 원래 제대로 출력되던 게 너무 많이 깨져서 포기했습니다. GFM을 Kramdown으로 바꾸는 데 성공한다면 링크나 이미지 뿐만 아니라 평범한 글에도 [attribute를 다는 문법](#attribute-달기)을 쓸 수 있는 등 장점이 많으니 attribute를 많이 달 것 같다면 바꾸는 게 좋을 것 같습니다. 이 포스트와 작성법이 살짝 달라질 수 있습니다. 다만 GFM은 문법이 상대적으로 엄격하게 되어 있어 대부분의 블로그 사이트가 GFM을 사용하고 있기도 합니다. 따라서 정말 귀찮은 게 아니면 GFM을 사용하는 게 나을 수 있습니다.

⠀이 포스트는 초보버전에서 뭉뚱그린 HTML과의 접점을 중심으로 설명할 예정입니다. HTML과 연결된 설명이므로 개발자도구를 켜서 직접 확인하며 따라오시는 게 좋습니다.

## 기본적인 글 작성법
### \<p>와 \<br>
⠀기본적으로 그냥 텍스트를 쓰면 그대로 \<p> 텍스트가 됩니다. 한 줄 띄어서 단락이 나뉘면 다음\<p>로 넘어가며, space 두 번 enter 한 번은 \<br>이 되어 같은 단락 다음 줄이 됩니다.

### 강조(\<em>, \<strong>)
```markdown
*기울게*  
**굵게**  
***굵고 기울게***  
_기울게_  
__굵게__  
___굵고 기울게___
```
*기울게*  
**굵게**  
***굵고 기울게***  
_기울게_  
__굵게__  
___굵고 기울게___

### \<u>
⠀Markdown에는 밑줄 문법이 없습니다. 따라서 날것의 HTML을 사용해야 합니다.
```html
<u>밑줄</u>
```
<u>밑줄</u>

### \<hN>
⠀글 앞에 #을 두면 \<hN>이 되며 #의 개수가 N이 됩니다.

### \<ol> - \<li>, \<ul> - \<li>
⠀글 앞에 N.을 두면 \<ol>, 글 앞에 -을 두면 \<ul>이 됩니다. \<ol>이 숫자 자체는 모르고 번호라는 것만 알기 때문에 무슨 수를 적든 상관이 없습니다. 번호 나열과 그냥 나열을 섞으면 가끔 위계가 무너지는데, 이 때는 단락을 나눠줘야 합니다.
```markdown
1. 일
    1. 일 일
    2. 일 이
3. 삼
    - 삼 1
    - 삼 2

- 1
    - 1 1
        - 1 1 1
- 2
```
1. 일
    1. 일 일
    2. 일 이
3. 삼
    - 삼 1
    - 삼 2

- 1
    - 1 1
        - 1 1 1
- 2

### \<blockquote>
⠀글 앞에 >을 붙이면 인용문이 됩니다. 단락을 나누지 않으면 > 하나로 단락 전체가 인용문에 들어갑니다.
```markdown
>이게 나야
```
>이게 나야

### \<code>
⠀글을 \`(백틱)로 묶으면 `이렇게`됩니다. 

⠀\`\`\`를 이용해 코드블럭을 만듭니다. 코드블럭은 꼬이는 경우가 많으므로 단락을 잘 나눠주는 게 좋은 것 같습니다.

```markdown
    ```markdown
    코드블럭 안 코드블럭
    ```
```

```html
<div class="language-markdown highlighter-rouge"><div class="highlight"><pre class="highlight"><button title="Copy to clipboard" class="clipboard-copy-button"><span class="sr-only">Copy code</span><i class="far fa-fw fa-copy"></i><i class="fas fa-fw fa-check copied"></i></button><code>코드블럭 안 코드블럭
</code></pre></div></div>
```

```markdown
코드블럭 안 코드블럭
```

CSS와 연결하려면 저리 복잡하게 나온 HTML도 확인합니다.

### \<table>
```markdown
|가운데 정렬|우측 정렬|좌측 정렬|좌측 정렬|
|:---:|---:|:---|---|
|내용내용내용|내용내용내용|내용내용내용|내용내용내용|
|내용|내용|내용|내용|
```

|가운데 정렬|우측 정렬|좌측 정렬|좌측 정렬|
|:---:|---:|:---|---|
|내용내용내용|내용내용내용|내용내용내용|내용내용내용|
|내용|내용|내용|내용|

### \<a>
```markdown
[태초마을이다!](#시작하며)  
[더 태초마을이다!!](https://raphaelshine.github.io/blog/blog-1-starting-tips/)  
[똑같은 태초마을이다!!](/blog/blog-1-starting-tips/)  
<https://raphaelshine.github.io>  
[이렇게 하면][변수 받아오듯이] 할 수도 있습니다.  
[참조링크]라고 합니다.

[변수 받아오듯이]: #a  
[참조링크]: /categories/#blog
```
[태초마을이다!](#시작하며)  
[더 태초마을이다!!](https://raphaelshine.github.io/blog/blog-1-starting-tips/)  
[똑같은 태초마을이다!!](/blog/blog-1-starting-tips/)  
<https://raphaelshine.github.io>  
[이렇게 하면][변수 받아오듯이] 할 수도 있습니다.  
[참조링크]라고 합니다.

[변수 받아오듯이]: #a  
[참조링크]: /categories/#blog

⠀페이지 내에서 이동한다면 #을 이용해 소제목으로 이동할 수 있고, 사이트 내에서 이동한다면 baseurl은 빼도 됩니다.

⠀고수용 HTML과 Liquid 포스트에서 설명했지만, 외부사이트로 연결할 때는 `rel='noopener noreferrer'` [attribute를 다는 게](#attribute-달기) 좋습니다.
### [\<img>]
```markdown
![지구는 네모낳습니다](/assets/images/TheEarthCapture.png){: .align-center width="50%"}
```
![지구는 네모낳습니다](/assets/images/TheEarthCapture.png){: .align-center width="50%"}
## Attribute 달기
⠀많은 필요에 의해 우리는 attribute를 달 줄 알아야 합니다. 두가지 방법이 있는데, 그냥 날것의 HTML을 써서 넣어 주는 것과, Markdown(Kramdown) 방식으로 넣는 것이 있습니다.

### Markdown 방식
⠀블록에 `{: }`을 붙이고 안에 attribute를 넣으면 됩니다. attribute의 자세한 종류에 대해서는 [HTML 고수용](/blog/blog-7-hard-html-and-liquid/#내용-tag)을 확인하십시오.
```markdown
[제 깃허브 프로필입니다.](https://github.com/RaphaelShine){:target='_blank' rel='noopener noreferrer'}
```
[제 깃허브 프로필입니다.](https://github.com/RaphaelShine){:target='_blank' rel='noopener noreferrer'}

⠀`_config.yml`에서 `kramdown.input`을 `Kramdown`으로 설정했다면, [Kramdown 공식 사이트](https://kramdown.gettalong.org/quickref.html){:target='_blank' rel='noopener noreferrer'}에 있는 기능을 다 사용할 수 있습니다. `GFM`의 경우 링크와 이미지에만 `{: }`를 달 수 있는데 반해, `Kramdown`이면 글에도 붙여서 title, id, style도 간단하게 붙일 수 있습니다. *블록에 붙여야 함 주의* 

### HTML 방식
⠀보통 Markdown에서 이 방식으로 attribute를 달게 되는 것은, `site.kramdown.input` 설정을 하지 않고도 글의 color, font-family와 같은 문자 스타일을 바꾸기 위함 혹은 id를 설정하기 위함입니다. 그래서 <span style="color:gold">이와</span> <span style='font-family:OngleipParkDahyeon'>같이</span> 작성합니다.
```html
그래서 <span style="color:gold">이와</span> <span style='font-family:OngleipParkDahyeon'>같이</span> 작성합니다.
```

- color는 색을, font-family는 폰트를 결정합니다. 
- color나 font-family의 자세한 설정은 [CSS의 쓰임]() 포스트에서 확인하십시오.

## 마무리
⠀Markdown도 귀찮은 부분이 많아서 VSCode의 단축어 snippets를 사용하는 것도 좋습니다. 

[\<img>]:/blog/blog-13-uploading-Image/

***
내가 공부한 포스트 중 좋은 곳!

|:---:|:---|
|[HEROPY. DEV](https://www.heropy.dev/p/B74sNE){:target='_blank' rel='noopener noreferrer'}|여기 되게 친절하고 쉬우면서 내용도 알찹니다. CSS도 여기서 읽어보렵니다.|