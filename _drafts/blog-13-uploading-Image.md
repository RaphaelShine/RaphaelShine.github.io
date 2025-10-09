---
title: "[Blog]13. 이미지 올리기"
excerpt: "Github Pages에 이미지 올리는 친절한 과정"

sort_key : 13
categories:
  - Blog
tags:
  - [Blog-포스팅-팁, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-08
last_modified_at: 2025-10-06
---

## 이미지에 붙일 수 있는 HTML Attribute
- 정렬  
  `.align-left` : 왼쪽으로 붙이기  
  `.align-right` : 오른쪽 붙이기  
  `.align-center` : 가운데 
- 크기  
  `width=""` : 가로 길이. `="70%"`처럼도 되고 `="400"`(픽셀)처럼도 된다.  
  `hight=""` : 세로 길이  
  참고로 둘 중 하나만 적어도 알아서 맞춰집니다.

## Directory 이용
⠀Jekyll이 정적으로 저장한 이미지 파일을 열기 때문에 빠르게 띄울 수 있습니다. 이미지 이름도 설정해야 하고 directory에 저장하는 과정이 필요하기 때문에 보통 이 방법은 가끔 필요할 때만 사용합니다.

⠀Minimal-Mistakes에는 assets/images/폴더가 있어 이곳에 넣으면 되겠습니다.

⠀markdown에서 다음과 같이 작성합니다.
```markdown
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}
```
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}

## url 이용
⠀url을 이용하면 이미지가 뜨기까지 1초정도 걸리는 것 같습니다.

### Github Project Issues 이용
⠀Issue에 comment로 이미지를 달아 자동으로 생성되는 url을 이용하는 방법입니다. Github에게 이미지 저장을 떠맡기는 편법이라고 할 수야 있긴 한데 Github는 강하니까! 괜찮겠죠!

⠀Issue 이용에 대한 포스트를 미래에 올릴지는 모르겠지만 올리게 되면 여기 링크를 달아 드리겠습니다. 지금은 여기서 Issue부터 설명하겠습니다.

⠀Issue는 원래 개발상황을 관리하는 Project 기능의 요소로, 어떤 버그나 개선사항에 대해 토의하는 기능입니다. Issue를 이용하기 위해선 먼저 Project가 필요합니다. Github에서 Projects로 들어갑니다. Repository 화면의 바에도 있습니다. New project 버튼을 누릅니다.

(Create project 사진)

⠀아무거나 상관 없습니다. 뭘 누르든 뭘 누르지 않고 X를 누르든 하면 Table이나 Board나 Roadmap view일 텐데, 상관 없고 Add item 누릅니다. Issue가 item입니다. 대충 제목을 짓고 나면 Issue가 만들어집니다.

(Issue 사진)

⠀이 comment에다 이미지를 넣으면 Github가 자동으로 url으로 바꿔주고, 이 url을 복사해서 쓰면 됩니다. 참고로 comment를 제거하든 issue를 제거하든 상관 없습니다. 주의할 것은 이 때 comment 작성란에 변환된 url을 복사하지 않고 그냥 comment를 올려버리면 url은 스틱스 강을 건넙니다. 이미지 또 넣어야 합니다.

(이미지 url 뽑는 사진)