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
last_modified_at: 2026-01-27

profiles:
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 1"
    title: "이런 진지한 폰트로 아무 소리나 적고 있습니다."
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 2"
    title: "지금은 예시니까 그렇고 진짜 쓸 때는 어울리리라 생각합니다."
  - url: https://i.namu.wiki/i/i2EnSwSx9soW7O1WUgOvhOWghXM-EqY3uI9N2V9kAN0guO1wcd7cC26nX-v05UQFyhIsfY9Yj-8G_0AZKGXAEn-g0qyLYNin_-it6fZ37L6Y5dMVo-RAnh5vKJMdIfwq_UWldIXxPNPyOdLAOSeSwg.webp
    image_path: /assets/images/TheEarthCapture.png
    alt: "힝 속았지"
    title: "왜 그런진 모르겠는데 가끔 url을 타고 넘어가지 않고 팝업이미지로 등장하는 url이 있습니다. 그러면 이미지와 팝업 이미지가 다르게 할 수도 있죠."
---

## 시작하며
⠀이미지를 올리는 방법들과, 포스트에 유튜브 영상 거는 법도 소개해 보겠습니다.

## Markdown 문법 이용(기본)
⠀이미지나 영상을 올리기 위해선 src라는 것을 붙여 줘야 합니다. src는 이미지나 영상의 링크가 될 수도 있고, 파일 위치를 나타낸 directory 구조일 수도 있습니다.

### Directory 구조
⠀Jekyll이 정적으로 저장한 이미지 파일을 열기 때문에 빠르게 띄울 수 있습니다. 이미지 이름도 설정해야 하고 directory에 저장하는 과정이 필요해 귀찮기 때문에 보통 이 방법은 가끔 필요할 때만 사용합니다.

⠀Minimal-Mistakes에는 assets/images/폴더가 있어 이곳에 넣으면 되겠습니다.

⠀markdown에서 다음과 같이 작성합니다.
```markdown
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}
```
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}

### 링크(url)
⠀markdown에서 다음과 같이 작성합니다.
```markdown
![이미지](https://github.com/user-attachments/assets/497f7b63-e289-4ca3-b01f-cd8176a32342){: .align-center width="70%"}
```
![이미지](https://github.com/user-attachments/assets/497f7b63-e289-4ca3-b01f-cd8176a32342){: .align-center width="70%"}

#### Github Project Issues 이용
⠀Issue에 comment로 이미지를 달아 자동으로 생성되는 url을 이용하면 굳이 블로그 디렉토리를 무겁게 하지 않을 수 있습니다. Github에게 부담을 떠맡기는 편법이라고 할 수야 있긴 한데 Github는 강하니까! 괜찮을 겁니다!

⠀Issue 이용에 대한 포스트를 미래에 올릴지는 모르겠지만 올리게 되면 여기 링크를 달아 드리겠습니다. 지금은 여기서 Issue부터 설명하겠습니다.

⠀Issue는 원래 개발상황을 관리하는 Project 기능의 요소로, 어떤 버그나 개선사항에 대해 토의하는 기능입니다. Issue를 이용하기 위해선 먼저 Project가 필요합니다. Github에서 Projects로 들어갑니다. Repository 화면의 바에도 있습니다. New project 버튼을 누릅니다.

{% include figure image_path="https://github.com/user-attachments/assets/56834963-520b-4fe8-bf44-be1f4004ce91"
   alt="loding..."
   caption="Create project 사진"
   class="align-center"
   popup=true
   style="width:700px" %}

⠀아무거나 상관 없습니다. 뭘 누르든 뭘 누르지 않고 X를 누르든 하면 Table이나 Board나 Roadmap view일 텐데, 상관 없고 Add item 누릅니다. 

{% include figure image_path="https://github.com/user-attachments/assets/fb117ba4-806e-411d-b22e-3f94e7ff89da"
   alt="loding..."
   caption="repository 연결 사진"
   class="align-center"
   popup=true
   style="width:700px" %}

⠀대충 제목을 짓고 repository 연결하고 나면 Issue가 만들어집니다.

{% include figure image_path="https://github.com/user-attachments/assets/1b1b5e39-2913-45c0-a3bb-a92b9e716488"
   alt="loding..."
   caption="Issue 사진"
   class="align-center"
   popup=true
   style="width:700px" %}

⠀참고로, Issue가 다른 repository에 연결된다면, Project의 Setting에 들어가서 Default Repository를 설정한 후 다시 시도하면 될 것 같습니다.

{% include figure image_path="https://github.com/user-attachments/assets/a3f9b4b8-e52c-44e8-ab08-e0cfaf870647"
   alt="loding..."
   caption="Project Setting 사진"
   class="align-center"
   popup=true
   style="width:400px" %}

⠀Issue의 comment에다 이미지를 넣으면 Github가 자동으로 url으로 바꿔주고, 이 url을 복사해서 쓰면 됩니다. 참고로 comment를 제거하든 issue를 제거하든 상관 없습니다. 주의할 것은 이 때 comment 작성란에 변환된 url을 복사하지 않고 그냥 comment를 올려서 이미지주소를 복사하면 글자가 조금 뻥튀기 됩니다. 수정하기를 누르면 살릴 수 있습니다.

{% include figure image_path="https://github.com/user-attachments/assets/cceb7954-4638-49f4-92ce-b635b20e5440"
   alt="loding..."
   caption="이미지 url 뽑는 사진"
   class="align-center"
   popup=true
   style="width:700px;" %}

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
⠀Minimal Mistakes에는 Liquid의 include 문법으로 불러올 수 있는 파일 중에 이미지를 멋들어지게 뽑아주는 파일들이 있습니다. figure는 한 장을, gallery는 여러 장을 멋들어지게 뽑아 줍니다.

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
- `class` : `align-left` 쓰면 왼쪽, `align-right` 쓰면 오른쪽에 붙음. `align-center` 쓰면 가운데는 아니지만 caption이 그림에 붙음. 
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
⠀front matter에 이런 식으로 넣습니다. `url`은 선택사항인데, 팝업 이미지를 넣습니다. 안 넣으면 팝업도 없습니다.
```yml
profiles:
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 1"
    title: "이런 진지한 폰트로 아무 소리나 적고 있습니다."
  - image_path: /assets/images/TheEarthCapture.png
    alt: "사진 2"
    title: "지금은 예시니까 그렇고 진짜 쓸 때는 어울리리라 생각합니다."
  - url: https://i.namu.wiki/i/i2EnSwSx9soW7O1WUgOvhOWghXM-EqY3uI9N2V9kAN0guO1wcd7cC26nX-v05UQFyhIsfY9Yj-8G_0AZKGXAEn-g0qyLYNin_-it6fZ37L6Y5dMVo-RAnh5vKJMdIfwq_UWldIXxPNPyOdLAOSeSwg.webp
    image_path: /assets/images/TheEarthCapture.png
    alt: "힝 속았지"
    title: "왜 그런진 모르겠는데 가끔 url을 타고 넘어가지 않고 팝업이미지로 등장하는 url이 있습니다. 그러면 이미지와 팝업 이미지가 다르게 할 수도 있죠."
```
⠀이런식으로 본문에 넣습니다.
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
⠀HTML tag를 이용합니다. 추가 include 파일도 있긴 한데 쓰는 법이 오히려 더 복잡한 것 같아 빼겠습니다.

(사진 gallery)
```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/jNQXAC9IVRw?si=FsiClRZQYOpdk57T" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
```
<iframe width="560" height="315" src="https://www.youtube.com/embed/jNQXAC9IVRw?si=FsiClRZQYOpdk57T" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>