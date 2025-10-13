---
title: "[Blog]14. Github Pages 댓글 만들기"
excerpt: "직접 댓글 기능을 만든다."

sort_key : 14
categories:
  - Blog
tags:
  - [Blog-뼈대, Blog-날먹, Blog-초보]

toc: true
toc_sticky: true

date: 2025-10-13
last_modified_at: 2025-10-13
---

## 시작하며
⠀댓글 기능을 만드는 건 스스로 코드를 만들어 하기에는 조금 복잡하기 때문에 보통은 댓글 기능을 제공해주는 플랫폼을 이용합니다. 쉽고 편한 방법을 원하신다면 [utterances 쓰는 법 알려주는 블로그](https://ansohxxn.github.io/blog/utterances/){:target='_blank' rel='noopener noreferrer'}나 [disqus 알려주는 블로그](https://devinlife.com/howto%20github%20pages/blog-disqus/){:target='_blank' rel='noopener noreferrer'}를 읽어보시면 되겠습니다.

⠀그러나 저는 저 플랫폼들이 다 마음에 들지 않아서 JavaScript 세계에 도전했습니다. JS는 정말 초등학교 다닐 적에 조금 해본 게 전부였으므로 지금 머리속에는 아무것도 들어있지 않았습니다. 그래서 ChatGPT를 열심히 굴려 결국 완성했는데, 제가 바이브 코딩을 얕봤다는 걸 깨달았습니다. 생각보다 중독적인 기분이었습니다. 원래는 AI가 다 해주면 하는 맛도 없고, AI가 어디서 오류를 낼지 몰라 오히려 머리가 더 아팠는데, 요즘 발전을 많이 했는지 오류를 뿜어내긴 하지만 오류 바로잡는 것도 계속 시도하다 보면 되고, 오류나는 비율도 확실히 줄어든 느낌입니다. 성공할 기대치가 높아지니, 오류나면 슬프고, 성공하면 기쁜 것이 이제 도박에 가까워져서 빠져나가기가 어려웠습니다. 프런트엔드의 종말이 온 것 같습니다.

⠀제가 만든 댓글이 어떻게 구성되는지 살펴보겠습니다.
- post에 달린다
- 깊이는 최대 1 (대댓글까지)
- 구글과 깃허브 계정 중 택1하여 로그인

- GitHub Issues를 이용해 내용을 올린다.
- Cloudflare Workers로 프록시 서버를 빌려 백엔드 역할을 한다.
- Google Cloud에서 API를 가져와 OAuth를 설정한다.
- 깃허브는 GitHub OAuth App을 이용한다.

## Github OAuth App 만들기

GitHub → Settings → Developer settings → GitHub Apps → New GitHub App

⠀Repository permissions
- Issues: Read & write
- Metadata: Read-only (자동 기본)
- 나머지는 No access
- Where can this GitHub App be installed?: Only on this account (무난)

⠀생성 후
- App ID 메모
- Generate a private key → .pem 다운로드 (한 번만 보여줌)
- Install App 버튼 → 대상 레포(RaphaelShine.github.io)에 설치
- 설치 완료 페이지 URL에 installation_id가 보입니다(또는 “Installed GitHub Apps” 화면에서 확인). 메모

⠀메모에 있어야 할 것
- GITHUB_APP_ID (숫자)
- GITHUB_INSTALLATION_ID (숫자)
- GITHUB_PRIVATE_KEY (PEM 전체 문자열)
- REPO_OWNER= 여러분 깃허브 닉네임
- REPO_NAME= 여러분 블로그 repository 이름

## Google OAuth 만들기

APIs & Services → Credentials → Create Credentials → OAuth client ID

- Application type : Web application
- 이름은 임의로. 예시) “Comments Web Client”
- Authorized JavaScript origins : "https://여러분깃허브닉네임.github.io" (블로그 실제 Origin)

⠀메모에 있어야 할 것
- GOOGLE_CLIENT_ID (url)
- SESSION_SECRET (충분히 긴 랜덤 바이트(최소 32바이트 이상)를 직접 생성해 둔다. `LC_ALL=C tr -dc 'A-Za-z0-9!@#$%^&*()_+=-' < /dev/urandom | head -c 48; echo`를 쓰면 랜덤 바이트 줌.)

## Cloudflare Workers 프로젝트 만들기

⠀[Cloudflare 로그인](https://www.cloudflare.com/ko-kr/){:target='_blank' rel='noopener noreferrer'}

⠀wrangler 설치 (없으면)

```
npm i -g wrangler
```

⠀새 프로젝트

```
mkdir comment-proxy && cd comment-proxy
npm init -y
npm pkg set type=module
npm i jose
wrangler init --yes
wrangler kv namespace create COMMENTS_RATELIMIT
wrangler kv namespace create SESSIONS
```

⠀결과로 나온 id는 잠시 뒤 `wrangler.jsonc`에 넣어야 합니다. Would you like Wrangler to add it on your behalf? yes.로 답했다면 굳이 수정할 필요 없습니다.

## wrangler.jsonc
여러개면 `src/index.ts`가 있는 디렉토리의 `wrangler.jsonc`를 씁니다.

⠀원래 있던 코드에 잘 맞춰 넣어 보십시오.
```
"$schema": "node_modules/wrangler/config-schema.json",
"name": "아무 이름",
"main": "src/index.ts",
"compatibility_flags": [
    "global_fetch_strictly_public"
],
"assets": {
    // The path to the directory containing the `index.html` file to be served at `/`
    "directory": "./public"
},
"observability": {
    "enabled": true
},
// -------- 여기가 핵심: 프록시가 참조할 환경 변수 --------
"vars": {
    "REPO_OWNER": "여러분 깃허브 닉네임",
    "REPO_NAME": "댓글 저장용 repository 이름",
    "ALLOWED_ORIGIN": "https://여러분깃허브닉네임.github.io" // 블로그 실제 Origin
},
// -------- KV로 레이트리밋 --------
"kv_namespaces": [
    {
        "binding": "COMMENTS_RATELIMIT",
        "id": "방금 나온 id"
    },
    {
        "binding": "SESSIONS",
        "id": "방금 나온 id"
    }
]
```
값 등록 (cmd 위치가 `src/`와 `wrangler.jsonc`를 담고 있는 폴더여야 함)
```
wrangler secret put GITHUB_APP_ID
wrangler secret put GITHUB_INSTALLATION_ID
wrangler secret put GITHUB_PRIVATE_KEY
wrangler secret put GOOGLE_CLIENT_ID
wrangler secret put SESSION_SECRET
```
붙여넣기가 안되면 Cloudflare 사이트에서도 수정 가능합니다.  
단, 시크릿은 Cloudflare에만 저장 (대시보드/wrangler secret put)  
절대 코드/레포에 넣지 마십시오.

## src/index.ts (Worker 코드)

⠀코드는 제 repository에서...

⠀배포
```
wrangler publish
```

⠀배포 결과로 워크스 도메인이 나옵니다(예: https://comment-proxy.yourname.workers.dev). 이 도메인(또는 바인딩한 커스텀 도메인)을 프런트에서 호출합니다.
```
const API_BASE = "https://<your-worker>.workers.dev";
```

## 프런트 코드 comments-providers/custom.html

⠀코드는 제 repository에서...

## 마무리
⠀GPT와 씨름한 이틀 간의 사투를 갈아서 대충 적었습니다. 잘못 적어버린 곳이 있을 수 있으니 의심되는 부분은 말씀 부탁드립니다.