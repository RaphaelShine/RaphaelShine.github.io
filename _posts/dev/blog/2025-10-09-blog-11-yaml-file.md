---
title: "[Blog]11. Jekyll의 YAML 파일"
excerpt: "Jekyll 디렉토리 구조의 머릿말(front matter), config.yml, data/에 대해 구체적으로 배우고 수정 내용을 알아본다."

sort_key : 11
categories:
  - Blog
tags:
  - [Blog-구체적으로, MMistakes]

toc: true
toc_sticky: true

date: 2025-10-09
last_modified_at: 2025-10-09
---
## Jekyll 디렉토리의 파일
### front matter
⠀이전 포스트에서 설명했지만, Jekyll은 어떤 파일이든 front matter 안의 내용을 YAML으로 처리합니다. 여기서 정의한 속성은 문서 내부나 외부에서 변수로 쓸 수 있습니다. 해당 페이지의 front matter 변수는 `page.변수명`으로 접근하고 사이트 범위의 변수는 `site.변수명`으로 접근합니다.
```Markdown
---
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
```
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