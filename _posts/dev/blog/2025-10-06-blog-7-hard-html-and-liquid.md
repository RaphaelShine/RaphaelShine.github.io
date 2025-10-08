---
title:  "[Blog]7. 고수용 HTML과 Liquid 설명"
excerpt: "HTML의 태그(tag)와 속성(attribute)의 종류를 자세히 정리하고 Liquid의 문법을 배운다."

sort_key : 7
categories:
  - Blog
tags:
  - [Blog-뼈대부터, Blog-고수]

toc: true
toc_sticky: true

date: 2025-10-05
last_modified_at: 2025-10-05
---

## 시작하며
⠀HTML은 기본적으로는 **정적**이기 때문에 이번 포스트의 길이가 YAML처럼 엄청 짧을 수 있었지만, 개발자들은 **Liquid**를 이용해 HTML을 동적으로 이용하는 방법을 만들었습니다. 그렇게 여러분의 공부량이 늘어나게 되었습니다~! 저도 마찬가지.......

## HTML
⠀<span style='font-family:OngleipParkDahyeon'>HTML을 제대로 한다면 head, body같은 것부터 해야겠지만 지금은 몰라도 알 바 아닙니다. 블로그 만드는 데 꼭 필요한 것만 설명하겠습니다.</span>  
⠀라고 초보 버전에는 되어 있겠지만 우리는 더 배웁시다. 직접 개발자도구 켜고 디버깅 하면서 해보려면 아는 게 좋을 겁니다. 결국엔 다른 모든 것의 결과가 HTML이므로 가장 중요하다고 볼 수도 있겠습니다. 이 포스트도 사실 깊게 들어간 것은 아니니 더 배우고 싶다면 [MDN](https://developer.mozilla.org/ko/){:target="_blank" rel="noopener noreferrer"}을 보십시오.

⠀이 페이지의 HTML입니다.

(HTML e.g.)

HTML은 대강
```html
<tag attribute>내용</tag>
```
이렇게 생긴 게 전부입니다.

⠀tag는 글 묶는 법 정도로 생각하면 되겠고, attribute는 tag에 붙은 속성으로, 세부사항을 결정합니다.

⠀tag는 종류에 따라 가질 수 있는 attribute가 다릅니다. 다음은 모든 tag가 공통적으로 가질 수 있는 attribute 중 중요한 몇 개만 모은 것입니다. custom attribute도 만들 수 있는 것 같은데 아직 필요치 않아 찾아보진 않았습니다.

|:---:|:---|
|`id=""`|CSS나 JS의 식별자|
|`class=""`|CSS나 JS의 식별자|
|`style=""`|CSS를 직접 사용. 인라인CSS라고 한다.|
|`lang=""`|내용의 언어 설정(검색엔진이 본다. <span title="ko-KR, en-US처럼 표기하는 표준 언어 태그">BCP47</span> )|
|`hidden`|렌더링하지 않음|
|`title=""`|<span title="이렇게 :)">마우스 올리고 있으면 나오는 텍스트</span>|
|`data-???`|커스텀 attribute. JS에서 dataset으로 접근|

⠀다음은 tag를 Markdown과 연관되므로 알아야 할 것과 그렇지 않더라도 정말 중요한 것으로 몇 개만 모은 것입니다. 참고로, tag는 묶음이 한 단락을 차지해 다음 tag부분은 줄이 바뀌는 경우와 한 단락 안에서 줄 바꿈 없이 내용을 묶는 경우가 있으며, 각각 블록과 인라인이라고 합니다. 또, &lt;/tag&gt;로 내용물을 감싸야 하는 것과 내용물이 없는 것으로도 나눌 수 있습니다.

### 기본적인 tag
- &lt;head&gt; :
  메타정보 넣는 곳
- &lt;body&gt; :
  본문 쓰는 곳
- &lt;meta&gt; :
  메타정보
- &lt;style&gt; :
  CSS 넣는 곳
- &lt;script&gt; :
  JS 넣는 곳

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
- &lt;ol&gt; - &lt;li&gt;, &lt;ul&gt; - &lt;li&gt; :
번호로 묶거나, 번호 없이 묶거나.
- &lt;br&gt; :
줄 넘김 (내용물이 없습니다.)
- &lt;hr&gt; :
가로줄 (내용물이 없습니다.)
- &lt;strong&gt; :
굵게 (&lt;b&gt;와 비슷한데, &lt;b&gt;와 달리 나레이터가 읽을 때도 강조해 읽는 효과가 있는 차이가 있다고 합니다.)
- &lt;a&gt; :
  링크 연결된 글.

  |:---:|:---|
  |`href=""`|링크나 디렉토리|
  |`target=""`|href를 어디서 열지 선택.<br>`_self`:(default) 이 페이지. `_blank`:새 페이지. `_parent`:부모 페이지. `_top`:전체 창.|
  |`rel=""`|보안설정. `noopener`:href로부터 사이트 조작 차단. `noreferer`:href에게 사이트 url 비공개.<br>(외부 페이지로 이동한다면 다 다는 게 이롭습니다.)|
  |`download`|href을 파일로 다운로드|
- &lt;img&gt; :

  |:---:|:---|
  |`src=""`|이미지 링크나 디렉토리|
  |`alt=""`|이미지 못 뜨면 보여줄 대체 텍스트|
  |`width=""`|가로 길이 (px 또는 %)|
  |`height=""`|세로 길이 (위와 동일)|
  |`decoding=""`|이미지 압축을 푸는 시점.<br>`sync`:동기. 다른 파일이 늦어지면 순서를 기다리느라 시간이 오래 걸림. <br>`async`:비동기. 빠르게 떠야하는 곳에 씀.<br>`auto`:(default) 알아서 결정.|
  |`loading=""`|로딩 시점. `lazy`:뷰포트에 가까워질 때. `eager`:바로바로|
- &lt;audio&gt;, &lt;video&gt;

  |:---:|:---|
  |`src=""`|오디오나 비디오의 링크 또는 디렉토리|
  |`poster=""`|재생 전 견본 이미지|
  |`width=""`|가로 길이 (px 또는 %)|
  |`height=""`|세로 길이 (위와 동일)|
  |`controls`|재생 컨트롤 표시|
  |`autoplay`|자동재생|
  |`loop`|반복|
  |`preload=""`|재생 전 데이터 준비 <br>`auto`:미리 다 준비. `metadata`:메타데이터만. `none`:준비 안 함.|
- &lt;button&gt; :
이건 후에 더 공부하면 정확히 수정하겠습니다. 아직 버튼이란 걸 어찌해줄지 모르겠네요.

  |:---:|:---|
  |`type=""`||
  |`disabled`||
  |`name=""`||
  |`value=""`||
  |`form=""`||
- &lt;link&gt;
- &lt;input&gt;, &lt;textarea&gt;, &lt;select&gt; :
입력창.

  |:---:|:---|
  |`type=""`|`text`:(default)그냥 텍스트<br>이건 너무 많아서 [여기서 확인](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/text){:target='_blank' rel='noopener noreferrer'}|
  |`name=""`|데이터 전송할 변수명|
  |`value=""`|데이터 기본값|
  |`placeholder=""`|힌트 텍스트|
  |`required=""`|필수 입력|
  |`readonly`|읽기 전용|
  |`disabled`|비활성화|
  |`maxlength=""`|최대 글자수|

## Liquid
⠀Liquid는 액체라는 뜻인 거 여러분 모두 아시리라 생각합니다. HTML은 구성이 변수의 변화에 따라 흐르지 않습니다. Liquid는 유동적으로 변수의 변화에 따라 HTML을 작성합니다. 즉, Liquid가 하는 일이 무엇인지 이름에서부터 드러나는 것입니다. (뇌피셜)

Liquid는 대강
```liquid
{% raw %}{% tag something parameter %}
{{ variable | filter }}
{% endtag %}{% endraw %}
```
이렇게 생긴 게 전부입니다.

⠀Liquid는 간단한 녀석이니 그냥 밑의 예시 한번씩 보면 이해될 겁니다.

⠀tag와 filter의 종류가 꽤 많아서 이 포스트에서는 몇몇 중요한 것만 곁다리로 설명하고(보통 이것만 있어도 됩니다.) 더 필요하다면 대신 [MS가 친절히 설명한 문서 링크](https://learn.microsoft.com/en-us/power-pages/configure/liquid/liquid-filters){:target="_blank" rel="noopener noreferrer"}를 드립니다.

### variable types
- variable  
  ⠀Liquid는 숫자, 문자열, 배열, object를 변수에 담을 수 있습니다. null이나 None은 nill이라고 하며 if문에서 false로 처리됩니다. 나머지는 전부 true입니다.
  ```liquid
  {% raw %}{% assign number = 1 %}
  {% assign floatingPoint = 3.1415926535897932384626 %}
  {% assign string = "히히" %}
  {% assign array = "첫째, 둘째, 셋째" | split:", "%}
  {% assign object = site.author %}
  {% assign void = nill %}
  {{ number }}
  {{ floatingPoint }}
  {{ string }}
  {{ array }}
  {{ object }}
  {{ void }}{% endraw %}
  ```
  ```
  {% assign number = 1 %}{% assign floatingPoint = 3.141592653589793238462643383279502884197169399375 %}{% assign string = "히히" %}{% assign array = "첫째, 둘째, 셋째" | split:", "%}{% assign object = site.author %}{% assign void = nill %}{{ number }}
  {{ floatingPoint }}
  {{ string }}
  {{ array }}
  {{ object.name }}
  {{ object.avatar }}
  {{ object.location }}
  {{ void }}
  ```

  ⠀<span style='font-family:OngleipParkDahyeon'>참고로 선언부는 빈칸으로 출력되어 가독성이 떨어지므로 실제로는 한줄로 붙여 썼습니다.</span>
- object  
  ⠀object는 `.`을 이용해 갖고 있는 property에 접근할 수 있습니다. 위의 `site.author`는 `site`라는 object의 `author`라는 property에 접근한 것입니다. 저 `site.author` 또한 object여서 `name`, `avatar`, `location` 등의 property를 갖습니다.
- variable 출력  
  ⠀변수를 중괄호 두 개로 묶으면 안에 넣은 변수를 출력합니다.
  ```liquid
  {% raw %}{{ 1 }}{% endraw %}
  ```
  ```
  {{ 1 }}
  ```
  
### filter
⠀변수 옆에 변을 놓으면 filter를 넣을 수 있습니다. 변수를 추가 조작합니다. 왼쪽부터 오른쪽으로 실행됩니다. 또한, type에 맞지 않는 filter가 적용될 때, 적절한 type로 변환 가능하다면 변환됩니다. 이런 식으로 type를 전환합니다.
```liquid
{% raw %}{% assign a = "100" %}
{% assign a = a | plus:1 %}
{% if 101 == a %}
변환됨
{% endif %}{% endraw %}
```
```
{% assign a = "100" %}{% assign a = a | plus:1 %}{% if 101 == a %}변환됨{% endif %}
```

### tags
#### &#123;% assign %&#125;  
```liquid
{% raw %}{% assign One = 1 %}
{{ One }}은 1입니다
{% assign One = One | plus:1 %}
{{ One }}은 1입니까?{% endraw %}
```
```
{% assign One = 1 %}
{{ One }}은 1입니다
{% assign One = One | plus:1 %}
{{ One }}은 1입니까?
```
#### &#123;% capture %&#125;  
```liquid
{% raw %}{% capture context %}
근데 그거 알아? 코딩 잘하면 기억력도 좋대~!
{% endcapture %}
{{ context }}{{ context }}{{ context }}{% endraw %}
```
```
{% capture context %}근데 그거 알아? 코딩 잘하면 기억력도 좋대~!{% endcapture %}{{ context }}{{ context }}{{ context }}
```
#### &#123;% if %&#125;  
```liquid
{% raw %}{% assign hasKey = true %}
{% assign handCount = 2 %}
당신은 손{{ handCount }}개의 사나이다
{% if hasKey %}
  {% if handCount = 2 %}
    당신은 열쇠로 손쉽게 문을 열었다.
  {% else if handCount == 1 %}
    당신은 열쇠로 손쉽게 문을 열었다.
  {% else if handCount == 0 %}
    당신은 열쇠로 "입"쉽게 문을 열었다. 두둥탁!
  {% else %}
    당신은 열쇠로 문을 뜯어냈다.
  {% endif %}
{% endif %}{% endraw %}
```
```
{% assign hasKey = true %}{% assign handCount = 2 %}당신은 손{{ handCount }}개의 사나이다
{% if hasKey %}{% if handCount == 2 %}당신은 열쇠로 손쉽게 문을 열었다.{% else if handCount == 1 %}당신은 열쇠로 손쉽게 문을 열었다.{% else if handCount == 0 %}당신은 열쇠로 "입"쉽게 문을 열었다. 두둥탁!{% else %}당신은 열쇠로 문을 뜯어냈다.{% endif %}{% endif %}
```
고수용이니 이정도는 알리라 생각하여 ==, != 같은 operator나 and, or 설명은 뺍니다.
#### &#123;% case %&#125; - &#123;% when %&#125;  
```liquid
{% raw %}{% assign hasKey = true %}
{% assign handCount = 0 %}
당신은 손{{ handCount }}개의 사나이다
{% if hasKey %}
  {% case handCount %}
  {% when 2 %}
    당신은 열쇠로 손쉽게 문을 열었다.
  {% when 1 %}
    당신은 열쇠로 손쉽게 문을 열었다.
  {% when 0 %}
    당신은 열쇠로 "입"쉽게 문을 열었다. 두둥탁!
  {% else %}
    당신은 열쇠로 문을 뜯어냈다.
  {% endcase %}
{% endif %}{% endraw %}
```
```
{% assign hasKey = true %}{% assign handCount = 0 %}당신은 손{{ handCount }}개의 사나이다
{% if hasKey %}{% case handCount %}{% when 2 %}당신은 열쇠로 손쉽게 문을 열었다.{% when 1 %}당신은 열쇠로 손쉽게 문을 열었다.{% when 0 %}당신은 열쇠로 "입"쉽게 문을 열었다. 두둥탁!{% else %}당신은 열쇠로 문을 뜯어냈다.{% endcase %}{% endif %}
```
#### &#123;% for %&#125;  
```liquid
{% raw %}{% assign hasKey = true %}
{% assign characters = "0,1,2,3,4,5" | split:"," %}
{% for character in characters %}
  {% assign handCount = character | plus:0 %}
  당신은 손{{ handCount }}개의 사나이다
  {% if hasKey %}
    {% case handCount %}
    {% when 2 %}
      당신은 열쇠로 손쉽게 문을 열었다.
    {% when 1 %}
      당신은 열쇠로 손쉽게 문을 열었다.
    {% when 0 %}
      당신은 열쇠로 "입"쉽게 문을 열었다. 두둥탁!
    {% else %}
      당신은 괴물이란 오해를 받아 열쇠를 빼앗겼다.
      {% assign hasKey = false %}
    {% endcase %}
  {% else %}
    당신은 열쇠가 없다...
  {% endif %}
{% endfor %}{% endraw %}
```
```
{% assign hasKey = true %}{% assign characters = "0,1,2,3,4,5" | split:"," %}{% for character in characters %}{% assign handCount = character | plus:0 %}
당신은 손{{ handCount }}개의 사나이다
{% if hasKey %}{% case handCount %}{% when 2 %}당신은 열쇠로 손쉽게 문을 열었다.
{% when 1 %}당신은 열쇠로 손쉽게 문을 열었다.
{% when 0 %}당신은 열쇠로 "입"쉽게 문을 열었다. 두둥탁!
{% else %}당신은 괴물이란 오해를 받아 열쇠를 빼앗겼다.
{% assign hasKey = false %}{% endcase %}{% else %}당신은 열쇠가 없다...
{% endif %}{% endfor %}
```
#### &#123;% include %&#125;  
```liquid
{% raw %}{% include page__meta.html %}{% endraw %}
```
{% include page__meta.html %}
`_include/` 디렉토리에 저장된 `page__meta.html` 파일을 가져와 붙여넣는 코드입니다. 파일 안에는 이 출력물의 HTML이 담겨 있고, 원래는 포스트 최상단에 있는 아이입니다.
#### &#123;% comment %&#125;  
```liquid
{% raw %}{% comment %}
아무말이나 적어도
{% endcomment %}
안보이지~{% endraw %}
```
```
{% comment %}
아무말이나 적어도
{% endcomment %}
안보이지~
```
주석입니다.
#### &#123;% raw %&#125;  
```liquid
{% raw %}{% raw %}
{% comment %}
아무말이나 적어도
{% endcomment %}
안보이지~
{% еndraw %}{% endraw %}
```
```
{% raw %}{% comment %}
아무말이나 적어도
{% endcomment %}
안보이지~{% endraw %}
```
이 아이가 바로 지금까지 Code부분을 작성하기 위해 쓴 tag입니다.  
<span style="font-family:OngleipParkDahyeon">재밌는 사실은 endraw는 중첩 시 앞에 있는 endraw가 바로 raw를 닫고 다음 endraw에서 오류를 내어 endraw를 출력할 수가 없는데, 이 위에 있는 Code는 라틴 알파벳과 똑같이 생긴 키릴문자를 이용해 회피했다는 것입니다. 이런 거 자주 쓰면 망합니다. 자주 쓸 수도 없지만~</span>

## 유의점, tip
⠀HTML이나 Liquid의 tag 때문에 진짜 <>나 {}는 본문에 쓰기 어려워 집니다. 그래서 이를 회피하기 위해 `&lt;`와 같이 HTML에서 지원하는 특수문자 치환 양식을 쓸 수 있습니다. [특수문자 치환표](https://dev-handbook.tistory.com/23){:target='_blank' rel='noopener noreferrer'}

⠀Markdown에서 HTML tag는 `\`를 이용해서도 작성이 가능합니다.
```markdown
\<strong>안녕?!</strong>
```
\<strong>안녕?!</strong>

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
***
내가 공부한 블로그!

|:---:|:---|
|[MS](https://learn.microsoft.com/en-us/power-pages/configure/liquid/liquid-overview){:target='_blank' rel='noopener noreferrer'}|블로그는 아니지만 Liquid는 여기서 제일 많이 배웠습니다.|
|[Higher의 창작소](https://higher77.tistory.com/93){:target='_blank' rel='noopener noreferrer'}|정적인 것과 동적인 것을 설명해 준 곳입니다. 아무래도 이런 건 버그랑만 놀아서는 알 길이 없으니 이렇게 알려주는 블로그가 중요했습니다.|