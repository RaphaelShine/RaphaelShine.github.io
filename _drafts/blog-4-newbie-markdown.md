---
title:  "[Blog]4. 초보용 Markdown 설명"
excerpt: "Markdown(마크다운)의 기본 작성법과 tip"

sort_key : 4
categories:
  - Blog
tags:
  - [Blog-뼈대부터, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-08
last_modified_at: 2025-10-08
---
## 시작하며
⠀Markdown은 HTML을 쉽게 쓰기 위한 텍스트 양식입니다. HTML은 tag붙이고 attribute넣고 하는 수고로움이 많지만 Markdown은 이 중 상당수를 쓰기 쉬운 기호로 대체합니다. 전부는 대체하지 못하므로 글을 이 이상으로 자유롭게 쓰고 싶다면 HTML을 배워야 합니다. `.md`확장자를 사용하며, HTML을 직접 써도 되고 따라서 Liquid도 작동합니다. <span style='font-family:OngleipParkDahyeon'>Liquid는 우선순위도 커서 Markdown의 코드블럭으로 봉인할 수 없습니다. 그래서 Liquid 문법 설명할 때 힘들어요ㅠㅠ</span> 또, 해석 방법이 다양해서 조금 들쭉날쭉 할 수 있습니다.

⠀이 포스트는 초보버전에서 뭉뚱그린 HTML과의 접점을 중심으로 설명할 예정입니다.

## 기본적인 글 작성법
### &lt;p&gt;와 &lt;br&gt;
⠀기본적으로 그냥 텍스트를 쓰면 그대로 &lt;p&gt; 텍스트가 됩니다. 따라서 단락은 다음&lt;p&gt;로 넘어가는 것으로, 같은 단락 다음줄은 &lt;br&gt;을 통해 실현됩니다. \<br>은 그냥 enter로 되지 않고, space 두 번과 enter로 인식됩니다.

### &lt;hN&gt;
⠀글 앞에 #을 두면 &lt;hN&gt;이 되며 #의 개수가 N이 됩니다.
```markdown
# 제목
```
### &lt;ol&gt; - &lt;li&gt;, &lt;ul&gt; - &lt;li&gt;
⠀글 앞에 N.을 두면 &lt;ol&gt;, 글 앞에 -을 두면 &lt;ul&gt;이 됩니다. \<ol>이 숫자 자체는 모르고 번호라는 것만 알기 때문에 무슨 수를 적든 상관이 없습니다. 번호 나열과 그냥 나열을 섞으면 가끔 위계가 무너지는데, 이 때는 단락을 나눠줘야 합니다.
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

### &lt;blockquote&gt;
⠀글 앞에 >을 붙이면 인용문이 됩니다. 단락을 나누지 않으면 > 하나로 단락 전체가 인용문에 들어갑니다.
```markdown
>이게 나야
```
>이게 나야

### &lt;code&gt;
⠀글을 \`(백틱)로 묶으면 `이렇게`됩니다. 

```html
<code class="language-plaintext highlighter-rouge">이렇게</code>
```

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

CSS와 연결하려면 저리 복잡하게 나온 attribute도 확인합니다.

### 표
```markdown
|:---:|:---:|
```

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
⠀링크와 이미지에는 Attribute를 달 수 있습니다. 그냥 글에도 달 수 있었다면 참 좋은데, 별의별 방법을 시도했지만 실패했습니다. 그냥 HTML을 쓰는 수밖에요.

⠀\[](){: }이렇게 붙이면 됩니다. 중괄호 안에는 전용 attribute 말고도 아무 거나 들어갈 수 있습니다. attribute의 자세한 종류에 대해서는 [HTML 고수용](/blog/blog-7-hard-html-and-liquid/#내용-tag)을 확인하십시오.

```markdown
[제 깃허브 프로필입니다.][새 탭으로 열리는 링크]{:target='_blank' rel='noopener noreferrer'}

[새 탭으로 열리는 링크]: https://github.com/RaphaelShine
```
[제 깃허브 프로필입니다.][새 탭으로 열리는 링크]{:target='_blank' rel='noopener noreferrer'}

[새 탭으로 열리는 링크]: https://github.com/RaphaelShine

## 마무리
⠀Markdown 파일은 지금 이 포스트를 포함하여, 블로그의 구체적인 모든 문서에 쓰입니다. 

⠀Markdown도 귀찮은 부분이 많아서 [VSCode의 단축어 snippets]를 사용하는 것도 좋습니다. 

[\<img>]:
[VSCode의 단축어 snippets]: 

***
내가 공부한 포스트!
|:---:|:---|
|[](https://www.heropy.dev/p/B74sNE){:target='_blank' rel='noopener noreferrer'}|