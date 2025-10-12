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

date: 2025-10-12
last_modified_at: 2025-10-12
---

1) GitHub App 만들기 (최소 권한)
GitHub → Settings → Developer settings → GitHub Apps → New GitHub App
Repository permissions
Issues: Read & write
Metadata: Read-only (자동 기본)
나머지는 No access
Webhooks: 지금은 비활성(나중에 필요하면 추가)
Where can this GitHub App be installed?: Only on this account (무난)
Create GitHub App 클릭
생성 후:
App ID 메모
Generate a private key → .pem 다운로드 (한 번만 보여줌)
Install App 버튼 → 대상 레포(RaphaelShine.github.io)에 설치
설치 완료 페이지 URL에 installation_id가 보입니다(또는 “Installed GitHub Apps” 화면에서 확인). 메모
정리해서 필요한 값:
GITHUB_APP_ID (숫자)
GITHUB_INSTALLATION_ID (숫자)
GITHUB_PRIVATE_KEY (PEM 전체 문자열)
REPO_OWNER=RaphaelShine
REPO_NAME=RaphaelShine.github.io


1) Cloudflare Workers 프로젝트 만들기

터미널에서:

# wrangler 설치 (없으면)
npm i -g wrangler

# 새 프로젝트
mkdir comment-proxy && cd comment-proxy
npm init -y

# ESM 사용을 위해 package.json에 type 지정
npm pkg set type=module

# JWT 서명 라이브러리
npm i jose

# wrangler 초기화 파일 생성
wrangler init --yes

2) KV(선택이지만 추천) — 간단 레이트리밋용
wrangler kv:namespace create COMMENTS_RATELIMIT


결과로 나온 id는 잠시 뒤 wrangler.toml에 넣어줄 거야.
3) KV 네임스페이스(선택·권장)

레이트리밋/스팸 방지에 간단히 쓰려고 KV를 하나 만듭니다.

wrangler kv:namespace create COMMENTS_RATELIMIT

4) wrangler.toml 설정
name = "comment-proxy"
main = "src/index.ts"
compatibility_date = "2024-05-01"

# 라우팅: 깃헙 페이지 도메인에서 프록시 경유라면, 별도 도메인/서브도메인 사용 추천
# 예: a.example.workers.dev 사용 또는 커스텀 도메인 바인딩
# routes = [{ pattern = "api.yourdomain.com/*", zone_id = "..." }]

[vars]
REPO_OWNER = "RaphaelShine"
REPO_NAME  = "RaphaelShine.github.io"
ALLOWED_ORIGIN = "https://raphaelshine.github.io" # 블로그 실제 Origin

# KV 바인딩
[[kv_namespaces]]
binding = "COMMENTS_RATELIMIT"
id = "<생성된_id_여기에>"


Secrets 등록:

wrangler secret put GITHUB_APP_ID
wrangler secret put GITHUB_INSTALLATION_ID
wrangler secret put GITHUB_PRIVATE_KEY


(프롬프트에 값 붙여넣기)

5) Worker 코드 (JWT 생성 → 설치 토큰 → 이슈 생성/조회 + CORS/레이트리밋)

src/index.ts

6) 배포
# 사전 점검
wrangler dev

# 배포
wrangler publish


배포 결과로 워크스 도메인이 나옵니다(예: https://comment-proxy.yourname.workers.dev).
이 도메인(또는 바인딩한 커스텀 도메인)을 프런트에서 호출합니다.
wrangler.toml의 ALLOWED_ORIGIN은 블로그 실제 오리진으로 맞추세요.

어떻게 나누면 되나?

블로그 레포 (Minimal Mistakes / Pages)

테마, 포스트, _config.yml, _layouts, 정적 리소스

프런트 JS 스니펫만 들어가면 됨
예: assets/js/comments.js 같은 파일에서

const API_BASE = "https://<your-worker>.workers.dev";


로 Worker를 호출

Worker 레포(별도)

src/index.ts, wrangler.jsonc, (옵션) package.json

배포는 wrangler deploy

이 레포는 공개여도 OK (시크릿이 파일에 없다는 전제)

단, 시크릿은 Cloudflare에만 저장 (대시보드/wrangler secret put)
절대 코드/레포에 넣지 마세요

Pages의 Functions 또는 Workers for Pages를 쓰는 구성이라면 Pages 레포에 워커 코드가 들어가지만, **우린 “독립 Worker”**를 쓰고 있으므로 완전히 분리가 깔끔합니다.

7) 프런트(블로그) 통합 — Minimal Mistakes에 삽입

보통 _includes/comments.html 혹은 포스트 레이아웃에 아래 스니펫 삽입

XSS 방지 위해 textContent 사용

8) 운영 팁(보안/스팸/운영)

절대 금지: 클라이언트에 GitHub 토큰/PAT 노출.

권한 최소화: GitHub App의 권한은 Issues: Read & write만.
레포도 댓글용 레포를 따로 두면 더 안전(운영 레포와 분리).

라벨로 포스트 매핑: labels: ["post:<id>"] 패턴 유지 → 한 포스트의 댓글만 조회 가능.

레이트리밋: 지금 예시는 IP당 60초에 5회. 필요시 강화(Cloudflare Turnstile, 추가 키(postId) 조합 등).

CORS: ALLOWED_ORIGIN을 블로그 도메인으로 고정. 여러 도메인이면 허용 목록 처리.

정렬/페이징: 댓글 많으면 page 파라미터 추가 구현.

알림: 이슈 생성 시 GitHub 알림이 자연스럽게 동작. 별도 EmailJS 필요 없음.

9) 체크리스트 (요약)

GitHub App 생성(권한 최소) + 설치 → APP_ID, INSTALLATION_ID, PEM 확보

Cloudflare Workers 프로젝트 생성 + jose 설치

wrangler.toml 설정 + Secrets/KV 등록

워커 코드 붙여넣고 wrangler publish

블로그에 프런트 스니펫 삽입(API_BASE 수정)

실제 포스트에서 댓글 등록/조회 테스트




내가 이전 GPT와 개발하던 내용이 너무 길어져서 새 대화를 시작하기 위해 이전 GPT가 너에게 남긴 인수인계 텍스트야. 핸드오버 요약 — “GitHub App + Cloudflare Worker 댓글 프록시” 현재 상태 아키텍처: GitHub Pages(블로그) + Cloudflare Worker(백엔드 프록시) + GitHub App(토큰 발급/Issues 쓰기). 배포 완료: Worker URL → https://wandering-cake-347a.raphaelshine.workers.dev 핸들러: GET /api/comments?postId=<id>(라벨 post:<id>가 붙은 Issues 목록) / POST /api/comments(이슈 생성). 시크릿/설정 Secrets: GITHUB_APP_ID, GITHUB_INSTALLATION_ID, GITHUB_PRIVATE_KEY(PKCS#8, 정상 반영됨). Vars: REPO_OWNER=RaphaelShine, REPO_NAME=RaphaelShine.github.io, ALLOWED_ORIGIN=https://raphaelshine.github.io CORS 강화 반영: 화이트리스트 + Vary: Origin + Access-Control-Max-Age: 86400. GitHub API 호출 시 User-Agent/X-GitHub-Api-Version 헤더 포함. KV 네임스페이스 COMMENTS_RATELIMIT 생성 및 간단 레이트리밋 적용(옵션). 동작 확인: GET 호출 시 {"items":[]} 응답까지 정상. POST로 이슈 생성되면 목록에 나타남. 디버그 엔드포인트: /__debug_keyhash (PEM 해시/형식 확인용) — 보안상 제거 권장. 코드 위치 Worker 레포(별도): src/index.ts, wrangler.jsonc → 블로그 레포에 푸시 불필요. 배포는 wrangler deploy. 블로그 레포: 댓글 위젯용 프런트 JS만 포함(예: assets/js/comments.js), API_BASE에 위 Worker URL 지정. 남은 과제 / 다음 단계 로그인/신원 표시 현재 익명 닉네임 입력만 지원. 로그인 기능은 아직 없음. 옵션: B1: GitHub OAuth(Cloudflare Worker에 OAuth 콜백 추가, 사용자 액세스 토큰으로 Issues 생성) → 실사용자 깃헙 계정으로 발행되므로 투명한 출처 표기 가능. B2: 외부 아이덴티티(Google Sign-In) 는 “표시용 프로필”에만 사용, 이슈 쓰기는 여전히 설치 토큰으로 대행(코멘트 바디에 signer 메타 저장). 후속 작업 시 세션/토큰 저장은 쿠키(httponly) 또는 Durable Objects/KV로. UI/디자인 커스터마이즈 현재는 JS가 HTML을 직접 삽입. Minimal Mistakes에 맞게 _includes/comments.html + assets/js/comments.js로 분리 권장. 해야 할 것: 목록 렌더 템플릿 (작성자, 시간 포맷, 마크다운/줄바꿈 처리) XSS 방어(텍스트 이스케이프 필수, 마크다운 라이브러리 사용 시 sanitize 옵션 ON) 빈 상태/오류 상태 UI 로딩 스피너/버튼 비활성화 등 UX 보안/운영 강화 Cloudflare Turnstile 추가(봇 방지) → Worker에서 검증 후 통과 시만 POST 허용. 레이트리밋 파라미터 조정(KV TTL/limit). /__debug_keyhash 제거 후 재배포. 필요한 경우 커스텀 도메인(route) 로 변경(예: api.yourdomain.com). 기능 확장(선택) 댓글을 Issue 코멘트로 저장(현재는 “각 댓글=Issue”)하도록 설계 변경 가능 → 1 포스트 = 1 Issue, 각 댓글 = Comments API (페이징 쉬움). 페이지네이션/정렬, 대댓글(Thread), 삭제/수정(권한 정책 필요), 알림(Webhooks → Worker → 메일/Discord 등). 엔드포인트 계약(현행) GET /api/comments?postId=<string> 200: { items: [{ id, number, title, body, created_at, user: { login } }] } 400: { error: 'Missing postId' } POST /api/comments 요청 바디: { title: string, body: string, postId: string } 201: { number: <issueNumber> } 400/429/5xx: { error: string } CORS: 허용 오리진 화이트리스트(배포 도메인 + 로컬 4000) 권한/설치 체크 요약 GitHub App Permissions: Issues = Read & write ✅ Install App: 대상 레포에 실제로 설치/선택됨 ✅ GITHUB_INSTALLATION_ID: 해당 설치의 ID(확인 끝) ✅ 시크릿은 모두 Cloudflare Secrets에만 저장, 레포/코드에 포함 금지 ✅ 유틸 명령(참고) # 배포 wrangler deploy # 로컬 개발 wrangler dev # 시크릿 관리 wrangler secret list wrangler secret put GITHUB_APP_ID wrangler secret put GITHUB_INSTALLATION_ID wrangler secret put GITHUB_PRIVATE_KEY # KV (필요 시) wrangler kv namespace list wrangler kv namespace create COMMENTS_RATELIMIT 요청 사항(다음 GPT에게) 로그인 기능 추가 설계(B1/B2 중 선택)와 구현 스캐폴드 제안 Minimal Mistakes에 맞춘 include + JS 리팩터링(템플릿/스타일 가이드 반영) Turnstile 통합 예제(프런트 & Worker 검증 코드) 댓글 저장 방식을 “1 포스트=1 Issue / 각 댓글=Issue Comment”로 바꾸는 마이그레이션 전략(선택) 이걸로 인수인계 끝! 이어서 로그인/디자인 쪽부터 다듬자 😊