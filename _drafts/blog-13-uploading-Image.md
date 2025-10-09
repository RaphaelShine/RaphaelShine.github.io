---
title: "[Blog]14. 이미지 올리기"
excerpt: "Github Pages에 이미지 올리는 친절한 과정"

sort_key : 14
categories:
  - Blog
tags:
  - [Blog-포스팅-팁, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-08
last_modified_at: 2025-10-06
---
## Directory 이용
Jekyll이 정적으로 저장한 이미지 파일을 열기 때문에 빠르게 띄울 수 있습니다. 이미지 이름도 설정해야 하고 directory에 저장하는 과정이 필요하기 때문에 보통 이 방법은 가끔 필요할 때만 사용합니다.

Minimal-Mistakes에는 assets/images/폴더가 있어 이곳에 넣으면 되겠습니다.

markdown에서 다음과 같이 작성합니다.
```markdown
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}
```
출력 :
![이미지](/assets/images/TheEarthCapture.png){: .align-center width="70%"}

붙일 수 있는 HTML Attribute
- 정렬
`.align-left` : 왼쪽으로 붙이기
`.align-right` : 오른쪽 붙이기
`.align-center` : 가운데
- 크기
`width=""` : 가로 길이. `="70%"`처럼도 되고 `="400"`(픽셀)처럼도 된다.
`hight=""` : 세로 길이
참고로 둘 중 하나만 적어도 알아서 맞춰집니다.

## Github Project Issues 이용
Issue에 comment로 이미지를 달아 자동으로 생성되는 url을 이용하는 살짝의 편법입니다. 이미지가 뜨기까지 1초정도 걸리는 것 같습니다.

