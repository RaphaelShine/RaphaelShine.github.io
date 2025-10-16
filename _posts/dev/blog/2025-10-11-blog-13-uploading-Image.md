---
title: "[Blog]13. 이미지 올리기"
excerpt: "Github Pages 블로그에 이미지 올리는 친절한 과정"

sort_key : 13
categories:
  - Blog
tags:
  - [Blog-팁, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-08
last_modified_at: 2025-10-14

profiles:
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 1"
    title: "이런 진지한 폰트로 아무 소리나 적고 있습니다."
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 2"
    title: "지금은 예시니까 그렇고 진짜 쓸 때는 어울리리라 생각합니다."
  - url: https://i.namu.wiki/i/-CanZXcv5h1jzxVVugyECmKkZN5kkmXU2fZ_AyFdpHRg58QeHscOoKLz7sBY1XH0OZO2USuQhuBlUSSubaeKlbS6d3M2j54vDzdG6g7gsy061auAN_3Hh8jk3m25S9ra4R7vCs55iMclQpNENQhr5A.webp
    image_path: /assets/images/TheEarthCapture.png
    alt: "힝 속았지"
    title: "왜 이렇게 만든진 모르겠는데 url을 설정하면 팝업 이미지는 다르게 설정할 수 있습니다."
---

## 시작하며
⠀이미지를 올리는 방법들과, 포스트에 유튜브 영상 거는 법도 소개해 보겠습니다.

## Markdown 문법 이용(기본)
⠀이미지나 영상을 올리기 위해선 src라는 것을 붙여 줘야 합니다. src는 이미지나 영상의 링크가 될 수도 있고, 파일 위치를 나타낸 directory 구조일 수도 있습니다.

### Directory 구조
⠀Jekyll이 정적으로 저장한 이미지 파일을 열기 때문에 빠르게 띄울 수 있습니다. 이미지 이름도 설정해야 하고 directory에 저장하는 과정이 필요하기 때문에 보통 이 방법은 가끔 필요할 때만 사용합니다.

⠀Minimal-Mistakes에는 assets/images/폴더가 있어 이곳에 넣으면 되겠습니다.

⠀markdown에서 다음과 같이 작성합니다.
```markdown
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}
```
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}

### 링크(url)
⠀url을 이용하면 인터넷에서 불러와야 하기 때문에 이미지가 뜨기까지 몇 초 더 걸리는 것 같습니다.

⠀markdown에서 다음과 같이 작성합니다.
```markdown
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}
```
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}

#### Github Project Issues 이용
⠀Issue에 comment로 이미지를 달아 자동으로 생성되는 url을 이용하면 굳이 블로그 디렉토리를 무겁게 하지 않을 수 있습니다. Github에게 부담을 떠맡기는 편법이라고 할 수야 있긴 한데 Github는 강하니까! 괜찮을 겁니다!

⠀Issue 이용에 대한 포스트를 미래에 올릴지는 모르겠지만 올리게 되면 여기 링크를 달아 드리겠습니다. 지금은 여기서 Issue부터 설명하겠습니다.

⠀Issue는 원래 개발상황을 관리하는 Project 기능의 요소로, 어떤 버그나 개선사항에 대해 토의하는 기능입니다. Issue를 이용하기 위해선 먼저 Project가 필요합니다. Github에서 Projects로 들어갑니다. Repository 화면의 바에도 있습니다. New project 버튼을 누릅니다.

(Create project 사진)

⠀아무거나 상관 없습니다. 뭘 누르든 뭘 누르지 않고 X를 누르든 하면 Table이나 Board나 Roadmap view일 텐데, 상관 없고 Add item 누릅니다. 

(repository 연결 사진)

대충 제목을 짓고 repository 연결하고 나면 Issue가 만들어집니다.

(Issue 사진)

⠀이 comment에다 이미지를 넣으면 Github가 자동으로 url으로 바꿔주고, 이 url을 복사해서 쓰면 됩니다. 참고로 comment를 제거하든 issue를 제거하든 상관 없습니다. 주의할 것은 이 때 comment 작성란에 변환된 url을 복사하지 않고 그냥 comment를 올려버리면 url은 스틱스 강을 건넙니다.

(이미지 url 뽑는 사진)

(스틱스 강 건넌 url 영상)

### 이미지에 붙일 수 있는 HTML attribute
- 정렬  
  `.align-left` : 왼쪽으로 붙이기  
  `.align-right` : 오른쪽 붙이기  
  `.align-center` : 가운데 
- 크기  
  `width=""` : 가로 길이. `="70%"`처럼도 되고 `="400"`(픽셀)처럼도 된다.  
  `hight=""` : 세로 길이  
  참고로 둘 중 하나만 적어도 알아서 맞춰집니다.

## 추가 include 파일 이용
⠀Liquid의 include 문법으로 불러올 수 있는 파일 중에 이미지를 멋들어지게 뽑아주는 것들이 있습니다. figure는 한 장을, gallery는 여러 장을 멋들어지게 뽑아 줍니다.

{% include figure image_path="/assets/images/TheEarthCapture.png"
   alt="profile"
   caption="네모로 각진 땅을 가진 지구 사진<br> (라임~)"
   class="align-left"
   popup=true
   style="width:170px" %}
### figure
- `image_path` : href
- `alt` : 이미지가 안 뜰 때 대신 나올 텍스트
- `caption` : title (이미지 설명)
- `class` : `align-left` 쓰면 왼쪽, `align-right` 쓰면 오른쪽에 붙음
- `popup` : 누르면 팝업
- `style` : (제가 수정해 만든 기능입니다.) 이제 style을 임의 지정할 수 있습니다.

<br>
```liquid
{% raw %}{% include figure
  image_path="/assets/images/TheEarthCapture.png"
  alt="profile"
  caption="네모로 각진 땅을 가진 지구 사진<br> (라임~)"
  class="align-left"
  popup=true
  style="width:170px" %}{% endraw %}
```

### gallery
⠀front matter에 이런 식으로 넣습니다.
```yml
profiles:
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 1"
    title: "이런 진지한 폰트로 아무 소리나 적고 있습니다."
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 2"
    title: "지금은 예시니까 그렇고 진짜 쓸 때는 어울리리라 생각합니다."
  - url: https://i.namu.wiki/i/-CanZXcv5h1jzxVVugyECmKkZN5kkmXU2fZ_AyFdpHRg58QeHscOoKLz7sBY1XH0OZO2USuQhuBlUSSubaeKlbS6d3M2j54vDzdG6g7gsy061auAN_3Hh8jk3m25S9ra4R7vCs55iMclQpNENQhr5A.webp
    image_path: /assets/images/TheEarthCapture.png
    alt: "힝 속았지"
    title: "왜 이렇게 만든진 모르겠는데 url을 설정하면 팝업 이미지는 다르게 설정할 수 있습니다."
```
⠀이런식으로 본문에 넣습니다. `url`은 선택사항인데, 팝업 이미지를 넣습니다. 안 넣으면 팝업도 없습니다.
```liquid
{% raw %}{% include gallery
  id="profiles"
  caption="지구가 네모낳다, 지구가 네모 낳다."
  layout="third" %}{% endraw %}
```
{% include gallery
  id="profiles"
  caption="지구가 네모낳다, 지구가 네모 낳다."
  layout="third" %}
- `id` : front matter에서 만든 gallery 이름
- `caption` : 이미지셋 설명
- `layout` : `half` 쓰면 두 줄, `third` 쓰면 세 줄, 다른 거 넣으면 한 줄, 안 넣으면 자동

⠀참고로 마우스 올렸을 때 테두리 나오는 색은 `_sass/minimal-mistakes/_page.scss/`의 `.page__content` 밑에 있습니다.
```scss
  a:not(.btn) {
    &:hover {
      text-decoration: underline;

      img {
        box-shadow: 0 0 10px rgba(#ffffff, 0.25); //여기 바꾸면 됩니다.
      }
    }
  }
```
## vidio 
⠀HTML tag를 이용합니다. 추가 include 파일이 있긴 한데 쓰는 법이 오히려 더 복잡한 것 같아 빼겠습니다.

(사진 gallery)
```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/jNQXAC9IVRw?si=FsiClRZQYOpdk57T" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
```
<iframe width="560" height="315" src="https://www.youtube.com/embed/jNQXAC9IVRw?si=FsiClRZQYOpdk57T" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>