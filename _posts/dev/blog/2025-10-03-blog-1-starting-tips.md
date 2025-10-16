---
title: "[Blog]1. Github Pages 시작하기"
excerpt: "블로그를 깃허브 페이지(Github Pages)로 시작하는 방법, 팁."

sort_key : 1
categories:
  - Blog
tags:
  - [Blog-뼈대, Blog-날먹, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-03
last_modified_at: 2025-10-13
---

## Github Pages란?
⠀블로그를 하려면 본인이 서버를 돌리거나 서버를 돌려주는 인터넷 서비스를 이용해야 합니다. 본인이 서버를 돌린다면 열심히 하는 만큼 다채롭고 자유로운 블로그를 만들 수 있겠지만, 인터넷 서비스를 이용하면 쉽고 편한 대신 정해진 템플릿을 벗어나는 데 어려움이 있거나 인터넷 서비스의 광고가 강제로 삽입됩니다.

⠀Github Pages는 Github에서 제공하는 인터넷 서비스입니다. 따라서 본인이 서버를 운영하는데 드는 부담이 없지만 다른 서비스들과 비교하여 차이가 있다면, Github에서는 <span style="color:yellow">**서버만**</span> 제공하기 때문에 <span style="color:yellow">**나머지는 스스로**</span> 코드를 올려줘야 합니다. 따라서 강제 광고도 없고 밑바닥부터 고칠 수 있습니다. 그렇기 때문에 Github Pages는 다른 서비스들에 비해 자유도가 굉장히 높습니다. 그게 제가 Github Pages를 택한 이유기도 합니다. 조금 수고하더라도 내가 밑바닥부터 다 뜯어 고칠 수 있길 바란다면 Github Pages를 선택하시면 됩니다.

⠀Github Pages에서는 기본적으로 Jekyll이라는 웹사이트 빌더를 사용합니다. 따라서 이후 포스팅은 Jekyll에 대한 설명이 주를 이룰 것이고, Github Pages가 아니더라도 Jekyll을 이용한다면 이 블로그의 내용이 도움이 될 수도 있겠습니다.

## 준비물

- [Github](https://github.com){:target="_blank" rel="noopener noreferrer"} 계정이 필요합니다.
- [Git](https://git-scm.com/downloads){:target="_blank" rel="noopener noreferrer"}이 필요합니다.  
  없어도 가능은 하지만 불편함이 너무 크므로 Git은 설치한 것을 전제하고 설명하겠습니다.
- Free 플랜에서는 public repository 1개만 지원합니다.  
  <span style="font-family:OngleipParkDahyeon">유료는 private도 되고 여러개도 된다네요~</span>
- 아무래도 깔끔한 코드 에디터 하나는 있어야 눈이 편합니다.  
  <span style="font-family:OngleipParkDahyeon">그냥 기본 텍스트 편집기를 써도 되기야 하지만...</span>  
  (전 [VisualStudioCode](https://code.visualstudio.com/download){:target="_blank" rel="noopener noreferrer"} 쓰는 중입니다.)
- 아무래도 브라우저가 있어야 합니다.
- 가장 중요한 건 열정!이 필요합니다.  

## 만든다

### 복붙하기

⠀[깃허브](https://github.com/topics/jekyll-theme){:target='_blank' rel='noopener noreferrer'}에서 마음에 드는 템플릿을 찾습니다. 혹시 템플릿을 기반하여 스스로 만드는 것도 귀찮거나 어렵다면 [이 블로그를 복사](https://github.com/RaphaelShine/RaphaelShine.github.io){:target='_blank' rel='noopener noreferrer'}하는 것도 방법입니다. 이 경우, 다 필요 없고 그냥 [Markdown 작성법](/blog/blog-4-newbie-markdown/)과 [자잘한 팁](/tags/#blog-팁)만 읽으셔도 되겠습니다.

⠀저는 [Minimal-Mistakes](https://github.com/mmistakes/minimal-mistakes){:target="_blank" rel="noopener noreferrer"}을 썼습니다. 앞으로 Minimal-Mistakes를 기준으로 설명할 계획입니다. 포스트 내용은 Jekyll의 공통적인 부분을 중심으로 설명할 테니 다른 템플릿으로 시작해도 큰 상관은 없지만 세부적인 디렉터리 구조를 설명할 때는 들어맞지 않을 수 있습니다.

![image](https://github.com/user-attachments/assets/7e294187-cc3b-4fef-8177-1b36b631c39a){: .align-center width="70%" height="70%"}

⠀Fork 버튼을 눌러 해당 repository를 fork합니다.

![image](https://github.com/user-attachments/assets/f2aa9f1a-441c-4430-8b1e-f43a9c62bb72){: .align-center width="70%" height="70%"}

⠀repository의 이름은 `여러분의 Github 아이디.github.io`로 짓습니다. 그래야 Github Pages를 이용한다고 인식합니다. <span style="font-family:OngleipParkDahyeon">(저는 이미 만들어놔서 빨개요...)</span>

⠀밑에 있는 <span style="color:green">Create Fork</span> 버튼을 누릅니다.

![image](https://github.com/user-attachments/assets/da6d2e84-2bb0-4fd0-b82f-17b561100dba){: .align-center width="70%" height="70%"}

리포지토리 > Settings > Code and automation > Pages를 확인합니다.

### 설정값 확인하기

![image](https://github.com/user-attachments/assets/9c9d9697-772d-45b9-933e-d7e7d6a8043a){: .align-center width="70%" height="70%"}

- Visit Site 버튼을 누르면 나오는 사이트가 이제 여러분의 블로그입니다.  
    <details><summary>(Visit Site 버튼이 나오지 않는다면?)</summary><div markdown="1">
    *변경사항을 만들어내야 합니다. 일단 코드를 수정하면 자연스럽게 나타납니다.*  
    *지금 바로 보고싶다면 밑에서 Branch를 None으로 변경했다가 Main(또는 Master)으로 돌아오십시오.*
    </div></details>
- Build and Deployment에서 설정한 Branch가 블로그를 구동합니다.  
    (Branch가 뭔지 모른다면? 그냥 넘어가십시오.)
- Custom domain을 이용하기 위해서는 추가 작업이 필요합니다.  
    도메인을 외부에서 설정 후 그 도메인을 기입하면 됩니다. [***자세한 내용***](https://docs.github.com/ko/pages/configuring-a-custom-domain-for-your-github-pages-site){:target="_blank" rel="noopener noreferrer"}

## 다듬는다 (Minimal-Mistakes 기준)

### 제거하기

⠀Fork해 온 상태 그대로는 사용하기 어렵습니다. 따라서 Github에 올라가 있는 파일을 여러분 컴퓨터로 옮겨와서 작업해 주셔야 합니다.

<details><summary>VSCode에서 Github 연동하는 법</summary><div markdown="1">
*좌측 바에서 Source Control을 찾아 <span style="color:cyan">Clone Repository</span> 버튼을 누릅니다.*  
*열린 창에서 Github 로그인 인증합니다.*  
</div></details>

![image](https://github.com/user-attachments/assets/5c138d0c-6d25-4cae-b355-e92928cc994d){: .align-center width="70%" height="70%"}

⠀Minimal-Mistakes의 경우 다음 파일들은 깔끔하게 제거할 수 있습니다. -[공식사이트 왈](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/){:target="_blank" rel="noopener noreferrer"}-

- .editorconfig
- .gitattributes
- .github
- /docs
- /test
- CHANGELOG.md
- minimal-mistakes-jekyll.gemspec
- README.md
- screenshot-layouts.png
- screenshot.png

### 수정하기

⠀여러분께서 깊이있게 들어가고 싶으시다면 다른 파일들도 건드리게 되겠지만, 기본적으로 수정해야 하는 부분은 다음 세 파트; `_config.yml`, `_posts`, `_pages` 입니다.

#### `_config.yml`
- 테마 설정  
  <span style="font-family:OngleipParkDahyeon">똑같이 해도 됩니다.</span>
```yml
# theme                  : "minimal-mistakes-jekyll"
remote_theme             : "mmistakes/minimal-mistakes"
minimal_mistakes_skin    : "default" #  "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"
```
- 블로그 프로필
```yml
# Site Settings
locale                   : "ko-KR"
title                    : "블로그 제목"
title_separator          : "-"
subtitle                 : "블로그 부제목"
name                     : "여러분 Github 아이디"
description              : "블로그 설명"
url                      : "https://여러분 Github 아이디.github.io"
repository               : "여러분 Github 아이디/여러분 Github 아이디.github.io" # repository 이름을 변경했다면 변경해야 합니다.
```
- 검색엔진 연동 <span style="font-family:OngleipParkDahyeon">나중에 다른 포스트로 빼야지...</span>  
  <span style="font-family:OngleipParkDahyeon">블로그가 검색엔진에서 발견되도록 합니다.</span>
```yml
# SEO Related
google_site_verification :
bing_site_verification   :
naver_site_verification  :
yandex_site_verification :
baidu_site_verification  :
```
- 여러분 프로필  
  <span style="font-family:OngleipParkDahyeon">좌측바에 보입니다.</span>
  <div markdown="1">
  ```yml
  # Site Author
  author:
    name             : "프로필에 걸고 싶은 여러분 이름"
    avatar           : # 프로필 사진, e.g. "/assets/images/프로필사진.png"
    bio              : "여러분 biography"
    location         : "Seoul, Korea"
    email            : "말그대로 email 주소"
    links: # 추가하고픈 건 추가할 수 있습니다.
      - label: "Email"
        icon: "fas fa-fw fa-envelope-square" # fas나 far는 기본 기호를 불러오는 아이입니다.
        url: "mailto:여러분.메일이름@이메일.com"
  ```
  </div>
- Outputting
```yml
# Outputting
permalink: /:categories/:title/
timezone: Asia/Seoul
date_format: "%Y/%m/%d" # 외국에서는 September 03, 2025 처럼 표시하잖아요? 그거 설정하는 겁니다. 
```
***참고 : 날짜 기호 표***

  ||연도|월|일|요일|  
  |:---:|:---:|:---:|:---:|:---:|  
  |전체숫자|`%Y`|`%m`|`%d`| |  
  |->|2025|10|03| |  
  |축약숫자|`%y`| |`%e`| |  
  |->|25| |3| |  
  |전체영문| |`%B`| |`%A`|  
  |->| |October| |Friday|  
  |축약영문| |`%b`| |`%a`|  
  |->| |Oct| |Fri|

  <span style="font-family:OngleipParkDahyeon">뇌절 좋아하는 분들을 위한 [제대로 된 표](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings){:target='_blank' rel='noopener noreferrer'}</span>

#### `_posts`
- 포스팅 해보기  
  >`_posts/` 폴더가 없다면 새로 만듭니다.  
  >`_posts/` 폴더 안에 파일을 새로 만듭니다.  
  >***파일의 이름은 `날짜-제목.md`으로 짓습니다.(`xxxx-xx-xx-title.md`)***  
  >다음 코드를 파일에 복붙하고 아무 글을 쓰십시오.
  
  ```markdown
  ---
  title:  "포스트 제목"
  excerpt: "포스트 소개"

  categories:
    - Amu_Category
  tags:
    - [Amu_Tag, Babo_Tag, Co_Tagzi]

  toc: true
  toc_sticky: true
  
  date: 2001-01-01
  last_modified_at: 2001-01-01
  ---
  <!--여기가 본문입니다. 이 밑으로 뭐든 써 보십시오.-->

  ```

#### `_pages`  
- 필수 페이지 만들기  
  >`_pages/` 폴더가 없다면 새로 만듭니다.  
  >`_posts/` 폴더 안에 `404.md` 파일을 넣습니다. 
  >주소를 찾지 못할 때 뜨는 페이지 입니다. 
  >`404.md` 파일이 없다면 새로 만듭니다.  
  >다음 코드를 파일에 복붙하십시오.

  ```markdown
  ---
  title: "Page Not Found"
  excerpt: "Page not found. Your pixels are in another canvas."
  sitemap: false
  permalink: /404.html

  layout: single
  ---

  <!--안타까운 메시지를 적어주십시오.-->
  아..! 정말 안타깝다!  
  페이지가 없다니..!  
  있는 줄 알고 들어온 내 페이지가..  
  내 페이지가...  
  페이지가 없다니...!

  <script>
  var GOOG_FIXURL_LANG = 'en';
  var GOOG_FIXURL_SITE = '{{ site.url }}'
  </script>
  <script src="https://linkhelp.clients.google.com/tbproxy/lh/wm/fixurl.js">
  </script>
  ```  
  >`_posts/` 폴더 안에 파일을 새로 만듭니다.  
  >***이름은 `category-archive.md`라고 짓습니다.***  
  >카테고리 목록이 뜰 페이지입니다.
  >다음 코드를 파일에 복붙하십시오.
  
  ```markdown
  ---
  title: "Category"
  layout: categories
  permalink: /categories/
  author_profile: true
  sidebar_main: true
  ---
  ```

## 확인한다
⠀수정 사항을 블로그에 반영하는 데 두 가지 방법이 있습니다. 

⠀<span style="color:lightblue">Github에 올려서</span> 사이트를 구동하는 것과, <span style="color:pink">로컬 서버</span>를 돌리는 것입니다.  

⠀사이트를 구동하기 위해서는 무조건 <span style="color:lightblue">Github에 올려야</span> 합니다. 그러나 Github에 코드를 올리면 Github는 구동에 <span style="color:lightblue">시간이 적잖이 소요됩니다.</span> 그래서 수정한 블로그가 잘 돌아가는지, 또는 포스트가 잘 올라가는지를 편히 확인하기 위해 <span style="color:pink">테스트용으로 로컬 서버</span>를 돌립니다. 당연히 로컬 서버에만 수정사항을 테스트하면 다른 사람들은 볼 수 없습니다.  

>로컬 서버를 돌리기 위해서는 준비 과정이 필요하므로 우선은 <span style="color:lightblue">Github로 push</span>하고 기다리는 것을 추천합니다.

1. <span style="color:lightblue">Github로 push.</span>
  - cmd의 위치가 `여러분 Github 닉네임.github.io`에 있는지 확인합니다.  
    <span style="font-family:OngleipParkDahyeon">다른 곳에 있다면 os에 맞는 명령어를 사용하여 이동합니다.  
    보통 `help` 치면 명령어 도움말이 나옵니다.</span>
  - cmd에 `git add .`을 입력합니다.  
    <span style="font-family:OngleipParkDahyeon">git의 initial setting은 끝낸 것을 전제하고 설명하겠습니다.  
    안 했으면 지금이라도 하세요!</span>
  - cmd에 `git commit -m "first commit"`을 입력합니다.  
  - cmd에 여러분의 branch에 따라 `git push origin master` 또는 `git push origin main`을 입력합니다.  
    <span style="font-family:OngleipParkDahyeon">여러분의 branch가 무엇인지는 `git status`를 입력해 나온 정보 중 찾거나 [repository setting](#설정값-확인하기){:target="_blank" rel="noopener noreferrer"}에서 찾을 수 있습니다.</span>
  - repository에서 파일 리스트 위에 여러분의 닉네임과 first commit이 적힌 곳 오른쪽, 체크박스가 <span style="color:green">체크</span>되기를 기다립니다.  
    
    ![image](https://github.com/user-attachments/assets/54ee3ec5-0773-4bdc-9c32-f6a1f9026d7f){: .align-center width="70%" height="70%"}

    <span style="color:orange">O</span>는 대기중, <span style="color:red">X</span>은 실패입니다.
2. <span style="color:pink">로컬서버를 돌린다.</span>  
  - Mac에서 shortcut  
    Mac은 아래 방법을 한 줄 씩 입력해 바로 로컬 서버 실행까지 가는 것도 가능합니다.  
    <span style="font-family:OngleipParkDahyeon">ruby 최신 버전이 업데이트 되었을 경우 3.2.9 대신 최신 버전을 쓰십시오.</span>
        ```bash
        brew install rbenv ruby-build
        echo 'eval "$(rbenv init -)"' >> ~/.zshrc
        source ~/.zshrc
        rbenv install -l
        rbenv install 3.2.9
        rbenv global 3.2.9
        ruby -v
        gem install bundler
        bundle -v
        gem install jekyll
        jekyll -v
        bundle install  

        bundle exec jekyll serve
        ```

    - [ruby](https://rubyinstaller.org/downloads/){:target="_blank" rel="noopener noreferrer"}를 다운 받습니다.  

    - bundler를 cmd를 통해 다운 받습니다.  
      ```bash
      gem install jekyll bundler
      ```
      확인 : `jekyll -v`
    - 로컬 서버를 실행합니다.
      ```bash
      bundle exec jekyll serve
      ```
    - 로컬 서버의 주소가 cmd에 뜨게 됩니다.  
      <span style="font-family:OngleipParkDahyeon">보통 <https://127.0.0.1:4000>입니다.</span>

⠀이제 한번 페이지를 둘러봅시다. 그리고 빈 곳을 어떻게 채울지, 무엇을 바꿀지 생각해 봅시다.

⠀계속되는 포스트에서 그 상상을 실현해 보겠습니다.

## 마무리
⠀이상 Github Pages를 시작하는 법이었습니다. 이후의 Blog 카테고리에선 Jekyll을 다룰 때 알아야 하는 부분들을 하나하나 세심하게 짚어 갈 예정입니다. 일단 Jekyll의 구조부터 markdown 문법이나 liquid 문법, 제가 만든 여러 기능들도 소개해 보겠습니다.

⠀저도 웹은 문외한이라 틀린 부분이나 개선사항이 있을 수 있습니다. 정정할 점이 보이는 똑똑이라면 꼭 **댓글**이나 [**메일**]({{site.author.email}}) 남겨 주셨으면 좋겠습니다. 그럼 칭찬과 감사 받으실 수 있겠습니다.

***
내가 공부한 포스트 중 좋은 곳!  

|:---:|:---|  
| [Hyeok-Jeong](https://velog.io/@jj770206/posts){:target="_blank" rel="noopener noreferrer"} | 여기서 별의별 블로그를 다 염탐했습니다. |  
| [공부하는 식빵맘](https://ansohxxn.github.io/categories/blog){:target="_blank" rel="noopener noreferrer"} | 위 블로그에서 찾은 곳인데, 상당히 깔끔해서 열심히 읽었습니다. 여기서 읽은 것들을 바로 적용하기에는 처음이라 잘 안됐지만 기본적인 개념들을 잡을 수 있었습니다. |  
| [SW Developer](https://devinlife.com/){:target="_blank" rel="noopener noreferrer"} | 여기를 읽을 때는 이미 위 블로그를 읽고 나서 ChatGPT와 단둘이 씨름하며 산전수전을 다 겪고 다 익숙해진 후이기에 사실 지금 필요한 정보를 얻은 건 아닙니다. 다만 검색엔진 등록이나 광고 등록 방법이 잘 돼있더군요. 나중에 이 부분 만들 때 읽으려고 갖다 두었습니다. |