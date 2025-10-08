---
title:  "[Blog]3. 초보용 HTML과 Liquid 설명"
excerpt: "HTML의 태그(tag)와 속성(attribute)의 종류를 쉽게 정리하고 Liquid의 문법을 간단히 알아본다."

sort_key : 3
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
⠀이번 포스트에서는 Jekyll이 다른 모든 코드들을 계산하여 결과물로 내놓는, 바로 HTML에 대해 배울 것입니다. HTML은 웹 개발 하면 나오는 세 묶음(HTML, CSS, JS)의 첫번째로, HTML에 쓰인 그대로 웹 페이지가 변화 없이 나타나게 됩니다. 이를 **정적**이라고 합니다. 반대로 **동적**인 것은 변수에 따라 페이지 구성이 변하는 것으로, 여러분이 입력한 아이디에 따라 웹 페이지에 보이는 여러분의 프로필이 달라지는 것을 예로 들 수 있겠습니다. 따라서 우리는 변수를 처리하기 위해 **정적**인 HTML이 아니라 동적인 Liquid라는 언어를 끼얹을 겁니다. Liquid는 HTML을 보조해 주기 위한 언어로, 변수처리를 하긴 하지만 단순히 HTML을 만드는 데만 쓰여 내용이 별로 없습니다. 그러니 만만하게 보고 아무렇게나 따라오셔도 되겠습니다.

## HTML
⠀HTML을 제대로 한다면 head, body같은 것부터 해야겠지만 지금은 몰라도 알 바 아닙니다. 블로그 만드는 데 꼭 필요한 것만 설명하겠습니다.

(HTML e.g.)

⠀이 페이지의 HTML입니다. 개발자 도구를 활용하면 내가 쓴 코드를 Jekyll이 어떻게 HTML로 나타냈는지 볼 수 있으니 버그가 있으면 원인을 찾을 때 유용하게 쓰실 수 있습니다. 읽으면서 개발자도구를 켜고 따라오시면 이해가 쉽습니다. chrome의 경우 ... > 도구 더보기 > 개발자도구로 열 수 있고, 개발자 도구의 HTML 창에 마우스를 올려 사이트 창에서 어디가 강조되는지로 해당 코드가 가리키는 부분을 볼 수 있습니다.

HTML은 대강
```html
<tag attribute>내용</tag>
```
이렇게 생긴 게 전부입니다.

⠀tag는 글 묶는 법 정도로 생각하면 되겠고, attribute는 tag에 붙은 속성으로, 세부사항을 결정합니다. 같은 tag로 묶인 서로 다른 두 글을 구별하기 위해 id나 class라는 attribute를 붙이는 식입니다.

⠀tag는 종류에 따라 가질 수 있는 attribute가 다릅니다. 다음은 모든 tag가 공통적으로 가질 수 있는 attribute 중 중요한 몇 개만 모은 것입니다. attribute는 `=""`의 따옴표 안에 변수를 넣는 것도 있고 변수를 받지 않는 것도 있습니다. 이렇게 입력받는 변수를 parameter[파라미터]라고 합니다.

|:---:|:---|
|`id=""`|CSS나 JS가 식별|
|`class=""`|CSS나 JS가 식별|
|`style=""`|글 스타일 지정|
|`lang=""`|내용의 언어 설정(검색엔진이 본다. <span title="ko-KR, en-US처럼 표기하는 표준 언어 태그">BCP47</span> )|
|`hidden`|렌더링하지 않음|
|`title=""`|<span title="이렇게 :)">마우스 올리고 있으면 나오는 텍스트</span>|
|`data-???`|커스텀 attribute.|

⠀다음은 tag 중 정말 중요한 것 몇 개만 모은 것입니다. 참고로, tag는 묶음이 한 단락을 차지해 다음 tag부분은 줄이 바뀌는 경우와 한 단락 안에서 줄 바꿈 없이 내용을 묶는 경우가 있으며, 각각 블록과 인라인이라고 합니다. 또, &lt;/tag&gt;로 내용물을 감싸야 하는 것과 내용물이 없는 것으로도 나눌 수 있습니다.

### 구역 tag
- &lt;header&gt; :
  머릿말 구역 e.g. 제목
- &lt;aside&gt; :
  사이드 구역 e.g. On This Page
- &lt;nav&gt; :
  네비게이션 e.g. 이 사이트 상단 바
- &lt;div&gt; :
  그냥 묶을 때 (블록)
- &lt;span&gt; :
  그냥 묶을 때 (인라인)
- &lt;article&gt; :
  하나의 글
- &lt;section&gt; :
  하나의 챕터 e.g. 소제목을 header로 갖는 여러 단락의 묶음
- &lt;footer&gt; :
  꼬리말 e.g. 출처

### 내용 tag
- &lt;h1&gt;, &lt;h2&gt;, &lt;h3&gt;, &lt;h4&gt;, &lt;h5&gt;, &lt;h6&gt; :
제목 (등수처럼, 수가 클수록 작은 제목입니다.)
- &lt;p&gt; :
단락
- &lt;ol&gt; - &lt;li&gt;, &lt;ul&gt; - &lt;li&gt;
번호로 나열하거나, 번호 없이 나열하거나. e.g. 지금 tag들이 나열되어 있는 것이 &lt;ul&gt; - &lt;li&gt;입니다. &lt;ol&gt;이나 &lt;li&gt;은 &lt;li&gt;들이 어떻게 나열되는지를 알 수 있도록 묶어 주는 역할입니다.
- &lt;br&gt; :
줄 넘김 (내용물이 없습니다.)
- &lt;hr&gt; :
가로줄 (내용물이 없습니다.) 가로줄이 사이트에 뜨는데 HTML에 &lt;hr&gt;이 없다면 그건 CSS에서 처리한 결과입니다. 다른 부분들도 그런 경우가 있으니 참고하고 CSS 배울 때 자세히 알아봅시다.
- &lt;strong&gt; :
**굵게** <- 이겁니다.

여기부턴 고유 attribute도 함께 설명하겠습니다.
- &lt;a&gt; :
  링크 연결된 글.

  |:---:|:---|
  |`href=""`|링크나 디렉토리|
  |`target=""`|href를 어디서 열지 선택. `_self`:(default) 이 페이지. `_blank`:새 페이지. `_parent`:부모 페이지. `_top`:전체 창.|
  |`rel=""`|보안설정. `noopener`:href로부터 조작 차단. `noreferer`:href에게 url 비공개.<br>(외부 페이지로 이동한다면 다 다는 게 이롭습니다.)|
  |`download`|href을 파일로 다운로드|

- &lt;img&gt; :

  |:---:|:---|
  |`src=""`|이미지 링크나 디렉토리|
  |`alt=""`|이미지 못 뜨면 보여줄 대체 텍스트|
  |`width=""`|가로 길이 (px 또는 %)|
  |`height=""`|세로 길이 (위와 동일)|

## Liquid
⠀Liquid는 액체라는 뜻인 거 여러분 모두 아시리라 생각합니다. HTML은 구성이 변수의 변화에 따라 흐르지 않습니다. Liquid는 유동적으로 변수의 변화에 따라 HTML을 작성합니다. 즉, Liquid가 하는 일이 무엇인지 이름에서부터 드러나는 것입니다. (뇌피셜) 코딩의 코자도 모른다고 간주하고 설명하겠습니다. 물론 ㅋ자는 안다고 생각하겠습니다.

Liquid는 대강
```liquid
{% raw %}{% tag something parameter %}
{{ variable | filter }}
{% endtag %}{% endraw %}
```
⠀이렇게 생긴 게 전부입니다. &#123;&#123; variable &#125;&#125;는 안에 있는 변수를 출력합니다. &#123;% tag %&#125;는 기능을 수행합니다.
⠀이제 중요한 tag들을 소개할 예정인데, 이건 어려우면 건너뛰고 나중에 필요할 때 어쩔 수 없이 돌아와도 됩니다.

### &#123;% assign %&#125;  
⠀Liquid는 숫자, 문자열, 배열, object, nill를 변수에 담을 수 있습니다. nill은 값이 존재하지 않음을 뜻합니다.
```liquid
{% raw %}{% assign One = 1 %}
{{ One }}은 1입니다
{% assign One = One | plus:1 %}
{{ One }}은 1+1입니다{% endraw %}
```
```
{% assign One = 1 %}
{{ One }}은 1입니다
{% assign One = One | plus:1 %}
{{ One }}은 1+1입니다
```
&#123;% assign %&#125;은 선언문입니다. 첫 줄은 One이라고 칭할 변수를 선언하고 One의 value를 1로 정했다는 의미입니다. 보면, Liquid만 적힌 줄이더라도 빈줄로 처리되는 것을 알 수 있습니다. 그래서 복잡한 코드가 아니면 보통 다 붙여서 씁니다.  
둘째 줄은 One의 값을 출력하니 1이 나왔고, 셋째 줄은 One의 value를 정하는데, One|plus:1 -> One+1 -> 1+1 -> 2로 정하겠다는 겁니다.  
넷째 줄에서 2가 출력되었습니다.
### &#123;% if %&#125;  
```liquid
{% raw %}{% assign hasKey = true %}
{% if hasKey %}
짤깍! 문을 열었다.
{% endif %}{% endraw %}
```
```
{% assign hasKey = true %}
{% if hasKey %}
짤깍! 문을 열었다.
{% endif %}
```
&#123;% if %&#125;는 조건문입니다. if 다음에 있는 변수가 true이면 내용물을 실행하고 false이면 실행하지 않습니다.
true나 false가 아니더라도 값이 존재하면 true로 판단하고 nill이면 false로 판단합니다.
### &#123;% for %&#125;  
```liquid
{% raw %}{% for field in site.data.navigation.main %}
{{ field.title }}
{% endfor %}{% endraw %}
```
```
{% for field in site.data.navigation.main %}
{{ field.title }}
{% endfor %}
```
&#123;% for %&#125;는 반복문입니다. in 다음에 있는 변수 밑에 있는 요소들을 차례로 빼와서 for와 in 사이에 둔 변수명으로 넣어 내용물을 각 요소들에 대해 반복하는 것입니다. `site.data.navigation.main`이라는 변수에 {% for field in site.data.navigation.main -%}{{- field.title -}}{{ "," -}}{%- endfor -%}가 요소로 포함되어 있는 것입니다.
### &#123;% include %&#125;  
```liquid
{% raw %}{% include page__meta.html %}{% endraw %}
```
{% include page__meta.html %}
`_include/` 디렉토리에 저장된 `page__meta.html` 파일을 가져와 붙여넣는 코드입니다. 파일 안에는 이 출력물의 HTML이 담겨 있고, 원래는 포스트 최상단에 있는 아이입니다.
## 유의점, tip
⠀HTML의 tag 때문에 진짜 <>는 본문에 쓰기 어려워 집니다. 그래서 이를 회피하기 위해 `&#123;`와 같이 HTML에서 지원하는 특수문자 치환 양식을 쓸 수 있습니다. [특수문자 치환표](https://dev-handbook.tistory.com/23){:target='_blank' rel='noopener noreferrer'}

⠀Markdown에서 HTML tag는 `\`를 이용해서도 작성이 가능합니다. Liquid의 중괄호엔 적용되지 못하지만 어차피 이중 중괄호나 중괄호 퍼센트를 쓸 일은 없어 보입니다. 그럼에도 쓰고싶다면 [고수 포스트]()를 확인하십시오.
```markdown
\<strong>안녕?!</strong>
```
\<strong>안녕?!</strong>

⠀
<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
***
내가 공부한 블로그!

|:---:|:---|
|[MS](https://learn.microsoft.com/en-us/power-pages/configure/liquid/liquid-overview){:target='_blank' rel='noopener noreferrer'}|블로그는 아니지만 Liquid는 여기서 제일 많이 배웠습니다.|
|[Higher의 창작소](https://higher77.tistory.com/93){:target='_blank' rel='noopener noreferrer'}|정적인 것과 동적인 것을 설명해 준 곳입니다. 아무래도 이런 건 버그랑만 놀다간 알 길이 없으니 이렇게 알려주는 블로그가 중요했습니다.|