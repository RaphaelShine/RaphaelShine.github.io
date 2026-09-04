---
title: "[Tools]3. Mac에서 윈도우 쓰는 법: VMware Fusion"
excerpt: "맥(Mac) 가상환경(Virtual Machine) VMware Fusion 소개와 사용법. 맥북에서 다른 운영체제(OS)를 구동해보자!"

sort_key : 3
categories:
  - Tools
tags:
  - [VMware Fusion]

toc: true
toc_sticky: true

date: 2026-09-04
last_modified_at: 2026-09-04

VMware bifurcation:
  - image_path: https://github.com/user-attachments/assets/eaf2bf47-63ba-4f02-805e-c225846f3bfb
    alt: "custom"
    title: "다운로드 받은 파일이 떠야 합니다."
  - image_path: https://github.com/user-attachments/assets/0ac5ea9a-5ee5-445e-aff4-8f7e82ce5c13
    alt: "get windows"
    title: "계속 진행하면 됩니다."
---
## 가상환경(Virtual Machine)이란?
⠀맥북을 샀는데 윈도우에서만 돌아가는 프로그램이 필요하다? 맥에서 윈도우를 돌리면 된다! 그걸 가능하게 하는 것이 바로 가상환경, 이 포스트에서 다룰 것은 그 중에서도 macOS의 대표격인 **VMware Fusion**입니다.

⠀<span style="font-family:OngleipParkDahyeon">가상환경에서는 막장을 저질러도 가상환경을 리셋하면 그만이기 때문에 위험한 일도 안전히 처리할 수 있는 유용한 도구이기도 합니다.</span>

## VMware Fusion 설치
### Broadcom
⠀먼저 [Broadcom](https://support.broadcom.com/web/ecx){:target="_blank" rel="noopener noreferrer"}에 로그인해야 합니다.
![로그인 시](https://github.com/user-attachments/assets/a3e2d08e-380b-4e49-b4ca-a0d51fe62e21){: .align-center width="70%" height="70%"}

⠀상단 바 우측의 로고를 눌러 메뉴를 VMware Cloud Foundation으로 전환, 좌측 검은 바 셋째칸 MyDownloads를 선택합니다.
![다운로드 창](https://github.com/user-attachments/assets/8a807fc0-9126-43c7-95b4-4b73a5c46271){: .align-center width="70%" height="70%"}

⠀청록색 표시 <span style="color:lightblue">Free Software Downloads available <u>HERE</u></span>에서 HERE로 들어가 Fusion을 검색합니다.
![두 Fusion 선택지](https://github.com/user-attachments/assets/be3d2966-2099-4c10-82c0-5f7079a47415){: .align-center width="70%" height="70%"}

⠀버전은 더 최신인 것, 더 멀쩡해 보이는 것으로 선택합니다. 이 포스트는 25H2 버전을 기준으로 작성되었습니다. Terms and Conditions를 읽어야 설치를 시작할 수 있습니다.
![설치 전 화면](https://github.com/user-attachments/assets/85373042-db7f-4bea-8841-177c5e2779bd){: .align-center width="70%" height="70%"}

⠀굉장히 귀찮지만 브로드컴은 Trade Compliance를 해줘야 합니다.
![Trade Compliance](https://github.com/user-attachments/assets/83255a8d-6ac9-4b6f-8545-cf8870c23134){: .align-center width="70%" height="70%"}

⠀굉장히 짜증나지만 Trade Compliance의 승인을 30분 이상 기다려야 합니다.
![기다려...](https://github.com/user-attachments/assets/2d08df3d-34d5-495a-a976-e2448fa8d75c){: .align-center width="70%" height="70%"}

⠀기다리는 동안 Windows Arm을 먼저 설치할 수 있습니다.

### Windows Arm 설치
⠀두 가지 방법이 있습니다. VMware 설치 후 VMware에서 Windows Arm을 설치하면서 시작하는 방법이 있고, 또는 미리 Windows Arm을 설치한 후 VMware에서 해당 파일을 선택하는 방법이 있습니다. 전자는 알 수 없는 이유로 Arm 설치가 완료되지 못하여 실패하는 경우가 있기 때문에 이 경우 후자의 방법을 사용해야 합니다.

⠀[Microsoft 사이트](https://www.microsoft.com/ko-kr/software-download/windows11arm64){:target="_blank" rel="noopener noreferrer"}에서 Windows Arm 파일을 다운로드 하면 됩니다.

## 가상환경 구동
### VMware
⠀VMware를 실행합니다. Windows Arm을 이미 설치했다면 custom을 선택, 안 했다면 get windows를 선택합니다.
![세 가지 선택지](https://github.com/user-attachments/assets/adfa640e-bc2a-40c2-9aec-8bd7725a76aa){: .align-center width="70%" height="70%"}

custom 이미지, get windows 이미지
{% include gallery
  id="VMware bifurcation"
  caption="각 케이스로 진행 시"
  layout="third" %}

⠀계속 진행하면 됩니다. 배당할 용량은 용도에 따라 다르겠지만 64GB면 보통 충분합니다.

### Windows 세팅
⠀VMware 세팅이 끝나면 Windows 세팅을 시작합니다. 그냥 진행하면 됩니다. 파일, 앱, 설정을 다 삭제한다고 겁먹지 말고 그냥 하면 됩니다. 별일 안 납니다.
![다 삭제한다!](https://github.com/user-attachments/assets/79168b82-cb6d-45ef-97b4-5c5af0ad5a27){: .align-center width="70%" height="70%"}
⠀가끔 인터넷 연결 부분에서 문제가 발생할 수 있습니다. `Shift` + `F10`을 통해 프롬프트창을 띄우고 `OOBE₩BYPASSNRO`를 명령합니다. 그러면 인터넷 연결을 건너뛰게 됩니다.
![인터넷 문제 발생 이미지](https://github.com/user-attachments/assets/628ae146-df20-4040-ba6f-546beea73d68){: .align-center width="70%" height="70%"}

### VMware tools 설치
⠀Windows 세팅을 끝냈다면 마우스 포인터 정상화와 인터넷 연결, 화면 해상도 최적화를 위해 VMware tools를 설치해야 합니다. 맥 최상단 바에서 `Virtual Machine` -> `Install VMware Tools` 누른 후 가상환경에서 파일을 열어 설치합니다.

## 마무리
⠀이제 맥북 들고 친구에게 가서 윈도우 프로그램 시전하면 아주 놀라겠죠. 여러모로 가상환경이 쓸모가 많습니다. 그럼 행복한 이중생활이 되시길 바랍니다.