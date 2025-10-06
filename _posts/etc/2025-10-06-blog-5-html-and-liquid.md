---
title:  "[Blog]5. HTML과 Liquid에 대한 적당한 설명"
excerpt: ""

sort_key : 0104
categories:
  - Blog
tags:
  - [Blog-뼈대부터, Blog-고수, MMistakes]

toc: true
toc_sticky: true

date: 2025-10-05
last_modified_at: 2025-10-05
---

## 시작하며
HTML은 기본적으로는 **정적**이기 때문에 이번 포스트의 길이가 저번 YAML처럼 엄청 짧을 수 있었지만, 동적 웹 페이지를 만들기 위해 개발자들은 **Liquid**이용해 HTML을 동적으로 이용하는 방법을 만들었습니다. HTML에 대해서는 딱히 볼 게 많지 않지만 Liquid의 문법이 조금 있습니다. 그렇게 여러분의 공부량이 늘어나게 되었습니다~! 저도.......

Liquid를 제대로 알기 위해서는 filter를 알아야 합니다. filter의 종류가 꽤 많아서 이 포스트에서는 다루지 않고 [MS가 친절히 설명한 문서로 링크](https://learn.microsoft.com/en-us/power-pages/configure/liquid/liquid-filters){:target="_blank" rel="noopener noreferrer"}를 드립니다.

## HTML
HTML을 제대로 한다면 head, body같은 것부터 해야겠지만 지금은 몰라도 알 바 아닙니다. 블로그 만드는 데 필요한 것만 설명하곘습니다.
라고 초보 버전에는 되어 있겠지만 우리는 더 배웁시다. 직접 개발자도구 키고 디버깅 하면서 해보려면 알아야 할 겁니다. 결국엔 다른 모든 것의 결과가 HTML이므로 가장 중요하다고 볼 수도 있겠습니다. 이 포스트로 부족하다면 [더 세세한 정보를 담은 이 블로그]()를 참고하십시오.

HTML은
```html
<tag attribute>내용</tag>
```
이게 답니다.

tag는 묶음법 정도로 생각하면 되겠고, attribute는 tag에 붙은 속성으로, 세부사항을 결정합니다.

이 페이지의 HTML입니다. 개발자 도구를 잘 활용하십시오.

(HTML e.g.)

tag는 블록과 인라인이 있는데, 블록은 한 줄을 차지하여 나가거나 들어올 때 줄이 바뀌어야 하고, 인라인은 줄 바꿈 없이 스며들 수 있습니다 또 종류에 따라 가질 수 있는 attribute가 다릅니다.

다음은 모든 tag가 공통적으로 가질 수 있는 attribute 중 중요한 몇 개만 모은 것입닌다.

|:---:|:---|
|id
|class
|style
|lang
|hidden
|title

다음은 tag를 대강 중요한 몇 개만 모은 것입니다. 

### 기본적인 tag
- &lt;head&gt;
  메타정보 넣는 곳
- &lt;body&gt;
  본문 쓰는 곳
- &lt;meta&gt;
  메타정보

### 구역 tag
- &lt;header&gt;  
  머릿말 구역 e.g. 제목
- &lt;aside&gt;  
  사이드 구역 e.g. On This Page
- &lt;nav&gt;  
  네비게이션 e.g. 이 사이트 상단 바
- &lt;div&gt;  
  그냥 묶을 때. 블록
- &lt;span&gt;  
  그냥 묶을 때. 인라인
- &lt;article&gt;  
  하나의 글
- &lt;section&gt;  
  하나의 챕터 e.g. 소제목을 header로 갖는 여러 단락의 묶음
- &lt;footer&gt;  
  꼬리말 e.g. 출처

### 내용 tag
- &lt;h1&gt;, &lt;h2&gt;, &lt;h3&gt;, &lt;h4&gt;, &lt;h5&gt;, &lt;h6&gt;  
제목 (등수처럼, 수가 클수록 작은 제목입니다.)
- &lt;p&gt;  
단락
- &lt;strong&gt;  
굵게. (&lt;b&gt;와 비슷한데, &lt;b&gt;와 달리 나레이터가 읽을 때도 강조해 읽는 효과가 있는 차이가 있다고 합니다.)
- &lt;br&gt;  
줄 넘김
>내용을 포함할 필요가 없으므로 &lt;/br&gt; 없이 혼자 씁니다.
- &lt;a&gt;  
  링크 연결된 글.
  |:---:|:---|
  |`href=""`|링크|
  |`target=""`|어디서 열지 선택. `_self`:(default) 이 페이지. `_blank`:새 페이지. `_parent`:부모 페이지. `_top`:전체 창.|
  |`rel=""`|보안설정. `noopener`:링크로부터 부모페이지 접근 차단. `noreferer`:링크에게 출처url 차단.|
  |`download`|url을 파일로 다운로드|
- &lt;img&gt;
  이미지. [구체적인 예시]()가 있는 포스트가 있습니다.
  |:---:|:---|
  |`src=""`|이미지 링크 또는 디렉토리|
  |`alt=""`|이미지 못 뜨면 보여줄 대체 텍스트|
  |`width=""`|가로 길이 (px 또는 %)|
  |`height=""`|세로 길이 (위와 동일)|
  |`loading=""`|로딩 시점. `lazy`:뷰포트에 가까워질 때. `eager`:바로바로|
  |`decoding=""`|
- &lt;audio&gt;, &lt;video&gt;  
오디오, 비디오. src, controls, autoplay, loop, poster, preload 등의 Attribute를 갖습니다.
  |:---:|:---|
  |`src=""`|
  |`controls`|
  |`autoplay`|
  |`loop`|
  |`poster=""`|
  |`preload=""`|
- &lt;button&gt;  
버튼. 
  |:---:|:---|
  |`type=""`|
  |`disabled`|
  |`name=""`|
  |`value=""`|
  |`form=""`|
- &lt;input&gt;, &lt;textarea&gt;, &lt;select&gt;  
입력창. type, name, value, placeholder, required, readonly, disabled, maxlength, checked 등의 Attribute를 갖습니다.
  |:---:|:---|
  |`type=""`|`text`:(default) `email`: `password`
  |`name=""`|
  |`value=""`|
  |`placeholder=""`|
  |`required=""`|
  |`readonly`|
  |`disabled`|
  |`maxlength=""`|
  |`checked`|
- data-*
custom attribute는 이렇게 작성하는 듯합니다.

## Liquid
