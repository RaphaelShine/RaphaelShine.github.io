---
title: "[Blog]4. 초보용 Markdown 설명"
excerpt: "Markdown(마크다운)의 기본 작성법과 팁."

sort_key : 4
categories:
  - Blog
tags:
  - [Blog-뼈대부터, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-09
last_modified_at: 2025-10-09
---
## 시작하며
⠀Markdown은 HTML을 쉽게 쓰기 위한 텍스트 양식입니다. HTML은 tag붙이고 attribute넣고 하는 수고로움이 많지만 Markdown은 이 중 상당수를 쓰기 쉬운 기호로 대체합니다. 전부는 대체하지 못하므로 글을 이 이상으로 자유롭게 쓰고 싶다면 HTML을 배워야 합니다. `.md`확장자를 사용하며, Markdown 파일에서도 HTML을 직접 쓸 수 있고 따라서 Liquid도 작동합니다. <span style='font-family:OngleipParkDahyeon'>해석 방법이 다양해서 조금 들쭉날쭉 할 수 있습니다.</span>

⠀Markdown은 어렵기가 어렵기 때문에 고수용도 읽어볼 수 있으면 좋습니다. 고수용에서는 HTML로 어떻게 나타나는지를 설명하고 있으니, HTML을 이해했고 **열정!**도 있다면 읽도록 하십시오. 글만 적는 데는 필요 없지만 스타일의 정확한 커스터마이징을 위해 필요합니다.

## 기본적인 글 작성법
### 단락
⠀기본적으로 그냥 텍스트를 쓰면 그대로 단락을 구성하게 됩니다. 다음 단락으로 넘어가기 위해선 enter 두 번으로 줄을 하나 띄웁니다. 같은 단락 다음 줄로 넘어가기 위해선 space 두 번 enter 한 번으로 이전 줄 끝에 space 두 개가 남아있어야 합니다.
```markdown
첫번째 단락입니다.

두번째 단락 첫째 줄입니다.
아직 첫째 줄입니다.  
이제 둘째 줄입니다.
```
첫번째 단락입니다.

두번째 단락 첫째 줄입니다.
아직 첫째 줄입니다.  
이제 둘째 줄입니다.

### 제목
⠀글 앞에 #을 두면 제목이 되고, #의 개수가 많을수록 작은 제목입니다. 
```markdown
#### 소제목
```
#### 소제목

### 강조
```markdown
*기울게*
**굵게**
***굵고 기울게***
```
*기울게*
**굵게**
***굵고 기울게***

### 밑줄
⠀Markdown에는 밑줄 문법이 없습니다. 따라서 날것의 HTML을 사용해야 합니다.
```html
<u>밑줄</u>
```
<u>밑줄</u>

### 번호 나열, 그냥 나열
⠀들여쓰기를 통해 위계를 갖습니다.
```markdown
1. 일
2. 이
  1. 이 일
  2. 이 이
- 1
- 2
  - 2 1
  - 2 2
- 3
```
1. 일
2. 이
  1. 이 일
  2. 이 이
- 1
- 2
  - 2 1
  - 2 2
- 3

### 인용문
⠀글 앞에 >을 붙이면 인용문이 됩니다.
```markdown
>이게 나야
```
>이게 나야

### 코드블록
⠀글을 \`(백틱)로 묶으면 `이렇게`됩니다. 다른 특수문자들이 실행되지 않게 해 주는 기능도 있습니다. `<span style='color:red'>이렇게 HTML 문법도 무시합니다.</span>`

⠀\`\`\`를 이용해 큰 코드블록을 만듭니다. 큰 코드블록은 꼬이는 경우가 많으므로 단락을 잘 나눠주는 게 좋은 것 같습니다.

```markdown
    ```markdown
    코드블럭 안 코드블럭
    ```
```

```markdown
코드블럭 안 코드블럭
```

### 표
```markdown
|가운데 정렬|우측 정렬|좌측 정렬|좌측 정렬|
|:---:|---:|:---|---|
|내용내용내용|내용내용내용|내용내용내용|내용내용내용|
|내용|내용|내용|내용|
```

|가운데 정렬|우측 정렬|좌측 정렬|좌측 정렬|
|:---:|---:|:---|---|
|내용내용내용|내용내용내용|내용내용내용|내용내용내용|
|내용|내용|내용|내용|

### 링크
```markdown
[태초마을이다!](#시작하며)  
[더 태초마을이다!!](https://raphaelshine.github.io/blog/blog-1-starting-tips/)  
[똑같은 태초마을이다!!](/blog/blog-1-starting-tips/)  
```
[태초마을이다!](#시작하며)  
[더 태초마을이다!!](https://raphaelshine.github.io/blog/blog-1-starting-tips/)  
[똑같은 태초마을이다!!](/blog/blog-1-starting-tips/)  

⠀\[글](링크)와 같이 적습니다.

⠀페이지 내에서 이동한다면 #을 이용해 소제목으로 이동할 수 있고, 사이트 내에서 이동한다면 baseurl은 빼도 됩니다.

⠀HTML과 Liquid 포스트에서 설명했지만, 외부사이트로 연결할 때는 `rel='noopener noreferrer'` [attribute를 다는 게](#attribute-달기) 좋습니다.
### [이미지]
```markdown
![지구는 네모낳습니다](/assets/images/TheEarthCapture.png){: .align-center width="50%"}
```
![지구는 네모낳습니다](/assets/images/TheEarthCapture.png){: .align-center width="50%"}

⠀!\[글](이미지)와 같이 적습니다. 위 예시와 같이 디렉토리로 넣을 수도 있고, 이미지 링크를 넣어도 됩니다. 저 중괄호가 무엇인가 하면,
## Attribute 달기
⠀링크와 이미지에는 attribute를 달 수 있습니다. HTML 설명할 때 졸았거나 건너 뛰었거나 기억이 안 날 여러분을 위해 설명드리자면, attribute라는 건 한국어로 속성이라고 하고, 그냥 tag에 다는 첨가물입니다. 링크를 눌러 타 사이트로 이동할 때 보안을 지켜주는 기능이나 이미지 크기와 정렬을 결정하는 기능을 합니다. 

⠀두가지 방법이 있는데, 그냥 날것의 HTML을 써서 넣어 주는 것과, Markdown 방식으로 넣는 것이 있습니다. 그 중 Markdown 방식은 링크와 이미지에만 사용할 수 있습니다.

### Markdown 방식

⠀`[](){: }`(링크) 또는 `![](){: }`(이미지) 이렇게 붙이면 됩니다.
```markdown
[제 깃허브 프로필입니다.](https://github.com/RaphaelShine){:target='_blank' rel='noopener noreferrer'}
```
[제 깃허브 프로필입니다.](https://github.com/RaphaelShine){:target='_blank' rel='noopener noreferrer'}

⠀링크로 본인 사이트로 이동 할 때는 그냥 적고, 타 사이트로 이동할 때는 이 attribute를 복사해서 붙여넣으십시오.

### HTML 방식

⠀보통 Markdown에서 이 방식으로 attribute를 달 때는 글의 color, font-family와 같은 문자 스타일을 바꾸기 위함입니다. 그래서 <span style="color:gold">이와</span> <span style='font-family:OngleipParkDahyeon'>같이</span> 작성합니다.

```html
그래서 <span style="color:gold">이와</span> <span style='font-family:OngleipParkDahyeon'>같이</span> 작성합니다.
```

## 마무리
⠀Markdown 파일은 지금 이 포스트를 포함하여, 블로그의 구체적인 모든 문서에 쓰입니다. 

⠀Markdown도 귀찮은 부분이 많아서 [VSCode의 단축어 snippets]를 사용하는 것도 좋습니다. 

[이미지]:
[VSCode의 단축어 snippets]: 

***
내가 공부한 포스트 중 좋은 곳!

|:---:|:---|
|[HEROPY. DEV](https://www.heropy.dev/p/B74sNE){:target='_blank' rel='noopener noreferrer'}|여기 되게 친절하고 쉬우면서 내용도 알찹니다. CSS도 여기서 읽어보렵니다.|