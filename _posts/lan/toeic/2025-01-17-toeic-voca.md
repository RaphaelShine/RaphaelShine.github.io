---
title: "[toeic] 단어장"
excerpt: 랜덤 순서 완전 사용자화 단어장

sort_key : 1
categories:
  - Toeic
tags:
  - [그냥 내가 필요해가꼬]

toc: true
toc_sticky: true

date: 2026-01-17
last_modified_at: 2026-01-17

vocab_groups:
  - id: "countability"
    title: "가산: Blue / 불가산: Red"
    list:
      # 혼동하기 쉬운 가산명사
      - { eng: "plan", kor: "계획", color: "b" }
      - { eng: "permit", kor: "허가증", color: "b" }
      - { eng: "fund", kor: "자금", color: "b" }
      - { eng: "approach", kor: "접근법", color: "b" }
      - { eng: "certificate", kor: "인증서", color: "b" }
      - { eng: "product", kor: "제품", color: "b" }
      - { eng: "process", kor: "과정", color: "b" }
      - { eng: "seat", kor: "좌석", color: "b" }
      # 혼동하기 쉬운 불가산명사
      - { eng: "planning", kor: "기획", color: "r" }
      - { eng: "permission", kor: "허가", color: "r" }
      - { eng: "funding", kor: "자금 조달", color: "r" }
      - { eng: "access", kor: "접근", color: "r" }
      - { eng: "certification", kor: "인증", color: "r" }
      - { eng: "production", kor: "생산", color: "r" }
      - { eng: "processing", kor: "처리", color: "r" }
      - { eng: "seating", kor: "좌석", color: "r" }
      # 기타 불가산
      - { eng: "information", kor: "정보", color: "r" }
      - { eng: "advice", kor: "조언", color: "r" }
      - { eng: "feedback", kor: "의견", color: "r" }
      - { eng: "equipment", kor: "장비", color: "r" }
      - { eng: "furniture", kor: "가구", color: "r" }
      - { eng: "consent", kor: "동의", color: "r" }
      - { eng: "merchandise", kor: "상품", color: "r" }
      - { eng: "machinery", kor: "기계류", color: "r" }
      - { eng: "knowledge", kor: "지식", color: "r" }
      - { eng: "change", kor: "잔돈", color: "r" }
      - { eng: "research", kor: "연구", color: "r" }
      - { eng: "news", kor: "뉴스", color: "r" }
      - { eng: "damage", kor: "손상", color: "r" }
      - { eng: "luggage", kor: "수하물", color: "r" }
      - { eng: "baggage", kor: "수하물", color: "r" }
      - { eng: "cash", kor: "현금", color: "r" }
  - id: "nouns_looking_like_adjectives"
    title: "형용사처럼 보이지만 명사로 쓰이는 어휘"
    list:
      # 모든 단어를 파란색(b)으로 설정
      - { eng: "alternative", kor: "대안", color: "b" }
      - { eng: "objective", kor: "목표", color: "b" }
      - { eng: "representative", kor: "대표자, 직원", color: "b" }
      - { eng: "professional", kor: "전문가", color: "b" }
      - { eng: "potential", kor: "잠재력", color: "b" }
      - { eng: "periodical", kor: "정기 간행물", color: "b" }
      - { eng: "approval", kor: "승인", color: "b" }
      - { eng: "disposal", kor: "처분", color: "b" }
      - { eng: "initiative", kor: "계획, 진취성", color: "b" }
      - { eng: "withdrawal", kor: "인출", color: "b" }
      - { eng: "appraisal", kor: "평가", color: "b" }
      - { eng: "referral", kor: "소개, 추천", color: "b" }
      - { eng: "arrival", kor: "도착", color: "b" }
      - { eng: "rental", kor: "임대", color: "b" }
      - { eng: "renewal", kor: "갱신", color: "b" }
      - { eng: "removal", kor: "제거", color: "b" }
      - { eng: "proposal", kor: "제안(서)", color: "b" }
      - { eng: "characteristic", kor: "특징", color: "b" }
---

<style>
  .vocab-container {
    max-width: 600px;
    margin: 40px auto;
    font-family: 'Pretendard', -apple-system, sans-serif;
  }

  .group-title {
    margin: 30px 0 15px;
    padding-left: 10px;
    border-left: 5px solid #333;
    font-size: 1.4rem;
    color: #e7e7e7ff;
  }

  .word-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 20px;
    margin-bottom: 10px;
    background: #ffffff;
    border: 2px solid #f0f0f0;
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .word-item:hover {
    background: #fafafa;
    border-color: #ddd;
  }

  /* 영단어: 항상 검은색 두껍게 */
  .word-eng {
    font-size: 1.2rem;
    font-weight: 800;
    color: #000000;
  }

  /* 뜻: 기본 숨김 */
  .word-kor {
    font-size: 1.05rem;
    font-weight: 700;
    visibility: hidden;
    opacity: 0;
    transition: opacity 0.2s;
  }

  /* 클릭 시 보임 */
  .word-item.show .word-kor {
    visibility: visible;
    opacity: 1;
  }

  /* 중립적 색상 정의 */
  .word-item.b .word-kor { color: #0056b3; } /* Blue (b) */
  .word-item.r .word-kor { color: #d63031; } /* Red (r) */
</style>

<div class="vocab-container">
  {% for group in page.vocab_groups %}
    <h2 id="{{ group.title }}" class="group-title">{{ group.title }}</h2>
    <div class="vocabulary-quiz" data-group-id="{{ group.id }}"></div>
  {% endfor %}
</div>

<script>
  (function() {
    // 1. Jekyll 데이터를 JSON으로 가져오기
    const allGroups = {{ page.vocab_groups | jsonify }};
    if (!allGroups) return;

    // 2. 화면에 배치된 모든 퀴즈 컨테이너 탐색
    const containers = document.querySelectorAll('.vocabulary-quiz');

    containers.forEach(container => {
      const groupId = container.getAttribute('data-group-id');
      const groupData = allGroups.find(g => g.id === groupId);

      if (groupData && groupData.list) {
        renderWords(container, [...groupData.list]);
      }
    });

    // 3. 단어 렌더링 함수
    function renderWords(target, list) {
      // 랜덤 셔플 (Fisher-Yates)
      for (let i = list.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [list[i], list[j]] = [list[j], list[i]];
      }

      list.forEach(item => {
        const itemDiv = document.createElement('div');
        // 중립적인 b/r 클래스 부여
        itemDiv.className = `word-item ${item.color}`;
        
        itemDiv.innerHTML = `
          <span class="word-eng">${item.eng}</span>
          <span class="word-kor">${item.kor}</span>
        `;

        // 클릭 토글 이벤트
        itemDiv.onclick = function() {
          this.classList.toggle('show');
        };

        target.appendChild(itemDiv);
      });
    }
  })();
</script>