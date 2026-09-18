---
title: "[Writing Poem] CrowView.cs"
excerpt: C#으로 쓴 시. 이상의 오감도를 C#으로 번역했다.

sort_key : 2
categories:
  - Writing-Poem
tags:
  - [현대시, 컴퓨터문학, C#]

toc: false

date: 2026-09-18
last_modified_at: 2026-09-18
---

```csharp
public class CrowView : BirdView {
    Child[] childrun = new Child[13];
    // Private is apposite

    void OnStreet() {
        childrun[0].Say("Imscared");
        childrun[1].Say("Imscared");
        childrun[2].Say("Imscared");
        childrun[3].Say("Imscared");
        childrun[4].Say("Imscared");
        childrun[5].Say("Imscared");
        childrun[6].Say("Imscared");
        childrun[7].Say("Imscared");
        childrun[8].Say("Imscared");
        childrun[9].Say("Imscared");

        childrun[10].Say("Imscared");
        childrun[11].Say("Imscared");
        childrun[12].Say("Imscared");
        int scaryChild=0, scaredChild=0;
        foreach (Child child in childrun) {
            if (child.isScary)
                scaryChild++;
            else if (child.isScared)
                scaredChild++;
            else
                throw new Exception("MuchBetterWithoutOtherReason");
        }

        if (scaryChild == 1);
        if (scaryChild == 2);
        if (scaredChild == 2);
        if (scaredChild == 1);

        // Public could be apposite
        childrun = null;
    }
}
```

## 역자의 말
⠀시를 이 꼴로 만들어 놓고 역자라는 것도 웃기다. 프로그래밍 언어로는 아무도 시를 쓰지 않았기 때문에 C#으로 쓴 시가 어떻게 생겨야 할지 그것은 개척자인 내 마음대로이다. 이미 번역이 아닌 오리지널 C# 시를 몇 개 짓긴 했으나 여기 올리기엔 부끄러울 정도로 가닥이 잡히지 않은 습작이기에 올리지 않는다. 한국의 현대시가 그러했듯 먼저 다른 언어로 된 시를 번역해 보는 것부터 시작한다. 뭐 어쩌면 이게 후에 많은 사람들이 읽게 될 프로그래밍 언어로 된 시의 시작일지도 모른다. 

⠀오감도(烏瞰圖)라는 제목은 조감도(鳥瞰圖)의 새 조鳥에서 획 하나가 빠진 모양이다. 이를 통해 까마귀의 이미지를 불러들여 시의 분위기를 조성한다. 이 언어유희적인 제목을 코드로 표현하는 것은 어렵다. 클래스명을 CrowView로 하고 BirdView(영어로 조감도)를 상속받게 했다. Bird에서 Crow로 상속되는 형태가 객체지향적으로 잘 맞아떨어진다고 보아 이렇게 의미는 전달했지만 언어유희를 담지 못해 아쉬웠다. 그래서 이 한은 첫 행에서 풀었다.

⠀`十三人의兒孩가道路로疾走하오.` Child의 Array로 13인의 아해를 표현했다. 이름은 childr**u**n으로 했는데 오탈자 같으면서도 疾走의 의미를 함축한다는 점에서 한을 제대로 풀었다고 생각한다.

⠀시에 괄호가 나오는데 이는 주석이나 throw new Exception()으로 바꾸었다. 여기엔 한글을 쓸 수 있었으나 프로그래밍 언어는 전 세계의 누구든 개발자라면 다 읽을 수 있다는 점이 큰 특징이라고 생각해 영어로 번역했다. 추가로 `막달은골목`이나 `뚫닌골목`을 각각 private와 public으로 바꾸었다. private과 public으로 은닉성을 고려하는 것이 중요한 객체지향형 언어에서는 시의 `막달은골목`이나 `뚫닌골목`이 나타내는 분위기가 private와 public에서 잘 나타난다고 생각했다.

⠀남은 부분은 모두 void OnStreet()의 body에 넣었다. 메서드로 한데 묶은 까닭은 시에서 표현하는 장면이 아해들이 말하는 것과 화자가 생각하는 것 뿐이기에 달리 구분될 부분이 없다고 본 것이다. 메서드명은 시의 배경인 골목 위의 일을 호출한다는 의미로 명명했다. 원래 클래스엔 메인함수나 public 메서드가 있어야 하므로 public을 붙일지 고민했으나 앞서 private is apposite라 했으므로 이를 살려 private로 두었다.

⠀이 시의 가장 충격적인 부분은 아마도 제1의 아해부터 모든 아해가 무섭다고 하는 걸 한 줄 한 줄 다 적은 것일 테다. 그러므로 반복문 없이 그대로 적었다.

⠀`十三人의兒孩는무서운兒孩와무서워하는兒孩와그러케뿐이모혓소.`에서는 반복문을 사용했는데, 이를 위해 본래 한 줄을 여러 줄로 늘린 것이 아쉽다. `모혓소`는 정말로 '모이다'라는 동사의 의미가 중요한 것이 아니라 존재하는 아해의 종류가 이러했다는 걸 말하는 것이다. 따라서 동사를 Gather()같이 메서드로 바꾸지 않았다. 대신 Child 클래스에 isScary와 isScared가 필드로 존재함을 상정하여 scaryChild와 scaredChild의 수를 각각 세는 형태로 바꾸었다.

⠀4연과 5연의 `...도 좃소`는 그것이 묘사가 아니라 별다른 효과를 산출하지 않는 생각의 형태이기에 고민을 많이 해야 했다. 그래서 4연에서는 정말 메서드를 호출하지 않고 조건문의 조건만 두었다. 정말 ...하여도 좋고 ...하여도 좋고 아무 상관이 없게 되는 코드가 되어서 의미가 살았다. 5연은 이와 전혀 다르게 바꾸었다. childrun은 질주의 의미와 아해의 존재 여부, 아해의 참조 등을 담고 있고, 또 클래스 안의 유일한 필드이기도 하다. 이런 childrun을 null로 만듦으로써 `十三人의兒孩가道路로疾走하지아니하야도좃소.`라는 문장의 의미를 잘 담았다고 생각한다.

⠀이로서 해설을 마친다. 이상의 시는 데카당적이라기에도 뭐한 참 신기한 난해시이기에 오히려 형식적인 부분에만 집중하여 번역하기에 편한 듯하다. 이후로는 더 서정적인 시를 번역하며 내용적으로도 프로그래밍 언어 시의 체계를 잡아야 할 것 같다.