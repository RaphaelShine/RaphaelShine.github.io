---
title:  "[Blog]5. 초보용 YAML 설명"
excerpt: "YAML을 통한 데이터 저장 방법을 배우고, Jekyll에서의 구체적인 활용을 알아본다."

sort_key : 5
categories:
  - Blog
tags:
  - [Blog-뼈대부터, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-05
last_modified_at: 2025-10-05
---
## YAML
⠀YAML은 JSON의 상위호환 데이터 직렬화 양식입니다.`.yml`, `.yaml`와 같은 확장자(둘 다 똑같습니다)를 사용합니다. 데이터 직렬화라는 것은 그냥 데이터 저장하기라고 생각하면 됩니다. 엄청 쉬우니 고수용은 따로 만들지 않겠습니다.

### 주석  
⠀#을 달면 주석처리 됩니다.
```yml
# ㅎㅎ
```
### 속성 선언
⠀key이라는 키에 value라는 값을 넣는 코드입니다.
```yml
key : value
```
⠀여러 값을 넣는 객체를 선언할 때는 들여쓰기를 이용합니다.
```yml
collections : 
  staff_members :
    permalink : /team/:name/
  books :
    permalink : /library/:name/
```
### 자료형
```yml
integer   : 3
string    : "엣헴" # " 없어도 string으로 인식합니다.
boolian   : true
array1 :
  - a1    : 1
  - b1    : 2
array2    : [1,"2",3,"4"]
date      : 2025-10-05
time      : 2025-10-05 14:47:15
```
⠀자세한 내용은 [나무위키](https://namu.wiki/w/YAML#s-3){:target="_blank" rel="noopener noreferrer"}에 되게 잘 되어 있습니다.
### 속성 접근
⠀YAML 파일을 저장한 후, 접근할 때는 `site.fordername.filename.key`와 같이 하면 됩니다. 파일이름 앞에 붙인 `_`는 빼고 적습니다. `_config.yml`은 특수한 파일이므로 `site.`에서 바로 접근합니다.
```liquid
{% raw %}{% if page.sort_key == 3 %}
  {{ site.data.navigation.main }}
{% endif %}{% endraw %}
```

***
⠀더 많은 내용이 필요하다면 댓글 남겨주십시오. 아는 선에서 최대한 답변드립니다.