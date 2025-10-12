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