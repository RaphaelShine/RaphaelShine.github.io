---
title: "[Blog]11. Jekyll의 YAML 활용, 파일 정리"
excerpt: "블로그에서 포스트 정렬하는 법, 제목 뒤에 이미지 띄우는 법을 배운다. Jekyll 디렉토리 구조의 머릿말(front matter), config.yml, data/에 대해 구체적으로 배우고 이 블로그에서 수정된 내용을 알아본다."

sort_key : 11
categories:
  - Blog
tags:
  - [Blog-구체적으로, MMistakes, Blog-날먹, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-09
last_modified_at: 2025-10-14
---
## 활용법
⠀YAML 문법에 대해 이해가 필요하다면 [여기](/blog/blog-5-newbie-yaml/)에 준비되어 있습니다.
### 포스트 정렬 기준 설정
⠀front matter에 변수를 하나 만듭니다.
```yml
sort_key : 11
```
⠀포스트를 나열하는 Markdown 파일에서 다음과 같이 `sort:""` filter에 변수명을 넣어주면 됩니다.
```liquid
{% raw %}{% assign posts = site.categories.Blog | sort: "sort_key" | reverse %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}{% endraw %}
```

### 제목 뒤쪽에 이미지 띄우기
⠀front matter에 다음과 같이 작성합니다.
```yml
header:
  overlay_image: # 이미지 src
  overlay_filter: 0.3 # 검게 0부터 1까지
  caption: "설명(우측하단)"
```
⠀수정을 원한다면 [`hero.html`](/blog/blog-10-html-file/#page__herohtml)을 수정하십시오.

## Jekyll 디렉토리의 파일들
⠀참고로 저는 Minimal-Mistakes를 fork해왔기 때문에 Minimal-Mistakes의 파일 기능과 그것을 어떻게 수정했는지를 중심으로 설명합니다. 이 템플릿을 쓰지 않았더라도 원하는 부분은 찾아서 가져가 쓰실 수 있습니다.
### front matter
⠀이전 포스트에서 설명했지만, Jekyll은 어떤 파일이든 front matter 안의 내용을 YAML으로 처리합니다. 여기서 정의한 속성은 문서 내부나 외부에서 변수로 쓸 수 있습니다. 해당 페이지의 front matter 변수는 `page.변수명`으로 접근하고 사이트 범위의 변수는 `site.변수명`으로 접근합니다.

<div class="language-markdown highlighter-rouge"><div class="highlight"><pre class="highlight"><button title="Copy to clipboard" class="clipboard-copy-button"><span class="sr-only">Copy code</span><i class="far fa-fw fa-copy"></i><i class="fas fa-fw fa-check copied"></i></button><code>---
title:  "[Blog]12. Jekyll의 YAML 파일"
excerpt: ""

sort_key : 12
categories:
  - Blog
tags:
  - [Blog-구체적으로, Blog-고수, MMistakes]

toc: true
toc_sticky: true

date:
last_modified_at: 2025-10-05
---
{% raw %}{% for tag in page.tags %}
{{tag}}
{{site.tags[tag].size}}
{% endfor %}{% endraw %}
</code></pre></div></div>

```
{% for tag in page.tags %}
{{tag}}
{{site.tags[tag].size}}
{% endfor %}
```
### `_config.yml`
⠀사용자 설정 속성을 담고 있습니다. 속성이 굉장히 많기 때문에 자세한 설명이 필요하면 그냥 [제 repository](https://github.com/RaphaelShine/RaphaelShine.github.io)의 `_config.yml`에서 주석을 확인하십시오.
### `_data/`
- 사이트 상단바를 navigation이라고 하며, Minimal-Mistakes 템플릿은 `navigation.yml`에 navigation에 있는 버튼들의 속성을 담습니다. 저는 다음과 같이 확장하고 [CSS]를 편집해 지금 여러분이 보고 계신 navigation을 만들었습니다. 
  <details><summary></summary>
  <div markdown="1">

  ```yml
  main:
    - title: "개발"
      name: "development"
      url: /development/
      children:
        - title: "유니티"
          name: "Unity"
          url: /development/unity/
        - title: "C#"
          name: "Csharp"
          url: /development/csharp/
        - title: "C"
          name: "C"
          url: /development/c/
    - title: "문학"
      name: "literature"
      url: /literature/
      children:
        - title: "시 창작"
          name: "Writing Poem"
          url: /literature/writing-poem/
        - title: "시 공유"
          name: "Sharing Poem"
          url: /literature/sharing-poem/
    - title: "언어"
      name: "language"
      url: /language/
      children:
        - title: "수어"
          name: "Korean Handsign"
          url: /language/korean-handsign/
    - title: "기타"
      name: "etc"
      url: /etc/
      children:
        - title: "블로그"
          name: "Blog"
          url: /etc/blog/
  ```
  </div></details>

- `ui-text.yml`에는 사이트 기본 단어들이 언어(컴퓨터 말고 자연어)별로 저장됩니다. 사이트 언어는 `_config.yml`에서 정하고, page나 post의 언어를 각각 따로 설정할 수도 있는 듯합니다. 저는 딱히 변경할 필요가 있어보이지 않아서 그대로 뒀습니다.


[CSS]: