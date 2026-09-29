---
title:  "[Unity]1. MonoBehaviour"
excerpt: "가장 기본적인 유니티 스크립트. MonoBehaviour는 무엇인가?"

sort_key: 1
categories:
  - Unity
tags:
  - [Unity, C#]

toc: true
toc_sticky: true
 
date: 2026-09-29
last_modified_at: 2026-09-29
---
## 시작하며
⠀온전한 이해를 위해선 상속에 대해 알고 있어야 한다.

⠀Unity는 GameObject라는 빈 껍데기에 Component들을 붙여서 기능을 동작시키는 **Component Pattern**을 사용한다. <span style="font-family:OngleipParkDahyeon">후에 디자인 패턴을 다루게 되면 링크를 걸도록 하겠다.</span> Component는 Transform과 Behaviour가 상속받는다. 여기서 Behaviour는 AudioSource, Collider, Camera, MeshRenderer 등이 상속받는다. 또한 MonoBehaviour도 Behaviour를 상속받는다.

```
UnityEngine.Object  
   └── Component  
         ├── Transform  
         └── Behaviour  
               ├── Camera, Light, AudioSource, Collider 등  
               └── MonoBehaviour
```

⠀Component는 Unity Editor에서 GameObject를 선택했을 때 Inspector에 나타나는 모든 것이다. Behaviour는 그 중 껐다 켰다 할 수 있는 것이다. 박스에 체크 표시로 On/Off 할 수 있다. Transform을 제외한 모든 Component가 Behaviour이다. 

⠀MonoBehaviour의 위치가 어느정도인지 감이 잡히는가? MonoBehaviour는 C# 코드를 Behaviour로 쓸 수 있도록 하는 클래스이다. 직접 작성한 C# class가 MonoBehaviour를 상속받게 하면 gameObject에 component로 넣을 수 있다. 위에서 설명한 상속관계 덕분이다.

## method
⠀처음 Unity에서 MonoBehaviour를 만들면 Start()와 Update()가 쓰여있다. 이들은 GameObject에 붙어 있는 MonoBehaviour라면 때에 따라 호출되는 기본 함수들이다. 저 둘 외에도 Awake(), OnGUI() 등의 기본 함수가 있다. 또한 On뭐시기()와 같이 조건에 따라 호출되도록 설정할 수 있는 함수도 만들 수 있다.

⠀이것이 가능한 이유는 C++로 구현된 엔진 내부에서 호출을 제어해주기 때문이다. 따라서 Unity에 작성한 모든 C# script들은 엔진에서 호출해 줄 수 있는 저 기본 함수들로부터 연결되어야 한다. 당연히 MonoBehaviour 없이 scripting을 할 수는 없다는 것이 된다.

⠀구체적으로 어떤 것들이 있는지는 [유니티 메뉴얼](https://docs.unity3d.com/Manual/event-functions.html){:target="_blank" rel="noopener noreferrer"}에서 확인할 수 있다.

## Inspector
⠀field에 public으로 선언되었으면 기본적으로 Inspector에서도 확인할 수 있다.

⠀field를 Inspector에서 확인할 수 있다는 것은 1. Editor에서 값을 할당 할 수 있고 2. 실행 중 값을 확인하거나 3. 실행 중 값을 임의로 변경할 수 있다는 의미가 있다.

⠀Inspector에 나타나는 것을 제어하기 위해 Unity Attributes를 사용할 수 있다.

```csharp
[SerializeField] // public이 아닌 것도 보여줌
[HideInInspector] // public인 것도 안 보여줌
[Space] // Inspector의 가독성을 위한 여백을 만듦
[Header("Header")] // Header를 닮
[Range(0,100)] // 수의 범위 설정, 슬라이더로 표기
[Tooltip("설명")] // 마우스 올리면 보이는 설명
[HelpURL("https://raphaelshine.github.io/")] // component 이름 옆 ?버튼을 누르면 이동
```

![GameManager in Inspector](https://github.com/user-attachments/assets/8f73b6a6-cf17-4266-9a18-b4ffed5c8403){: .align-center width="100%"}

<details><summary>실제 코드</summary><div markdown="1">

```csharp
[HelpURL("https://raphaelshine.github.io/")] // component 이름 옆 ?버튼을 누르면 이동
public class GameManager : MonoBehaviour
{
    [SerializeField] // public이 아닌 것도 보여줌
    private int privateNumber;
    
    [HideInInspector] // public인 것도 안 보여줌
    public int publicNumber;

    [Space(10)] // Inspector의 가독성을 위한 여백을 만듦
    public string stayAway;

    [Header("Header")] // Header를 닮

    [Range(0,100)] // 수의 범위 설정, 슬라이더로 표기
    public int slider;

    [Tooltip("설명")] // 마우스 올리면 보이는 설명
    public int needDescription;
}
```

</div></details>

## 참고할 특징
⠀MonoBehaviour는 new 키워드로 생성할 수 없다. 반드시 `gameObject.AddComponent<>();`를 사용한다. 이 때문에 Factory pattern을 구현할 때 생각을 좀 더 해야 한다.

⠀기본 함수라고 부른 것들 외에도 MonoBehavior 상속으로 사용할 수 있는 method들이 있는데 대표적으로 Instantiate<>()나 StartCoroutine()이 있다. property인 gameObject도 MonoBehavior에서 사용할 수 있다.

⠀MonoBehaviour는 C# script 안에 딱 그 class 하나만 있어야 한다.

## 마치며
⠀개발을 하다 보면 MonoBehaviour여야 할 class가 있고 아닌 것이 있다. 객체지향을 잘 하기 위해선 상속을 올바르게 해야 한다. 과연 이 클래스는 gameObject에 붙어서 함수 호출을 받아야 할지, 아니면 다른 MonoBehaviour 안에서 엔진의 호출 없이 구현을 도울지, 생각해보고 상속하도록 하자.