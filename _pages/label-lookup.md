---
title: 라벨 검색
permalink: /label-lookup/

layout: default
---

<section class="label-lookup">
  <h1>라벨로 포스트 찾기</h1>
  <p>이슈 라벨(예: <code>post:3f6b2d8c1a4e9d10</code>)을 입력하면 해당 포스트를 찾아 링크를 보여줍니다.<br>
  ※ 댓글 시스템과 동일하게 <strong><code>{% raw %}{{ page.id | slugify }}{% endraw %}</code></strong>를 해시합니다.</p>

  <div class="lookup-card">
    <label for="label-input">라벨</label>
    <input id="label-input" type="text" placeholder="post:xxxxxxxxxxxxxxxx 또는 16자리 해시" autocomplete="off">
    <button id="lookup-btn">검색</button>
  </div>

  <div id="result" class="result"></div>
</section>

<style>
  .label-lookup { max-width: 720px; margin: 2rem auto; font-family: system-ui,-apple-system,Segoe UI,Roboto,sans-serif; }
  .lookup-card {
    display: grid; gap: .6rem;
    background: #0f1115; color: #e5e7eb;
    border: 1px solid #232733; border-radius: 12px;
    padding: 1rem 1rem 1.2rem;
  }
  .lookup-card input {
    padding: .6rem .75rem; font-size: 16px;
    border: 1px solid #2a3040; border-radius: 8px;
    background: #0b0d12; color: #f3f4f6; outline: none;
  }
  .lookup-card input::placeholder { color: #6b7280; }
  .lookup-card button {
    width: 100%; padding: .65rem 1rem; border-radius: 8px;
    border: 1px solid #334155; background: #1e293b; color: #e2e8f0; cursor: pointer; font-weight: 600;
  }
  .lookup-card button:hover { background: #243041; }
  .result { margin-top: 1rem; }
  .result .ok { background:#0e1015; border:1px solid #263041; border-radius:10px; padding:.9rem; }
  .result .fail { color:#fca5a5; }
  .result a { color:#93c5fd; text-decoration:none; }
  .result a:hover { text-decoration:underline; }
  .suggestions { margin-top:.6rem; font-size:.95em; color:#a1a1aa; }
  code { background:#111318; padding:.1rem .35rem; border-radius:6px; border:1px solid #232733; }
</style>

<script>
(function(){
  // 1) 사이트의 모든 포스트 목록 (slugified id 사용!)
  const posts = [
    {% for post in site.posts %}
      { 
        id_slug: {{ post.id | slugify | jsonify }},   /* 댓글 시스템과 동일한 입력 */
        url: {{ post.url | absolute_url | jsonify }},
        title: {{ post.title | jsonify }}
      }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  // 2) SHA-256 → hex
  async function sha256Hex(input) {
    const enc = new TextEncoder().encode(String(input));
    const buf = await crypto.subtle.digest('SHA-256', enc);
    return Array.from(new Uint8Array(buf)).map(b => b.toString(16).padStart(2,'0')).join('');
  }
  async function makeSafeLabel(id_slug) {
    const h = await sha256Hex(id_slug);
    return 'post:' + h.slice(0, 16);
  }

  // 3) 라벨 맵 구성 (댓글 시스템과 동일 로직)
  const labelMap = new Map(); // label -> post
  const ready = (async () => {
    for (const p of posts) {
      const lab = await makeSafeLabel(p.id_slug);
      labelMap.set(lab, p);
    }
  })();

  // 4) 입력 정규화
  function normalizeInput(raw) {
    const s = String(raw || '').trim().toLowerCase();
    if (!s) return '';
    if (/^post:[0-9a-f]{16}$/.test(s)) return s;
    if (/^[0-9a-f]{16}$/.test(s)) return 'post:' + s;
    return s;
  }

  // 5) UI
  const $input = document.getElementById('label-input');
  const $btn = document.getElementById('lookup-btn');
  const $out = document.getElementById('result');

  function escapeHtml(s) {
    return String(s)
      .replace(/&/g,'&amp;').replace(/</g,'&lt;')
      .replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;');
  }
  function setResult(html) { $out.innerHTML = html; }

  async function lookup() {
    await ready;
    const norm = normalizeInput($input.value);
    if (!/^post:[0-9a-f]{16}$/.test(norm)) {
      setResult('<p class="fail">라벨 형식이 올바르지 않습니다. 예: <code>post:3f6b2d8c1a4e9d10</code></p>');
      return;
    }
    const post = labelMap.get(norm);
    if (post) {
      setResult(
        '<div class="ok">'
        + '<div>일치하는 포스트를 찾았습니다.</div>'
        + '<div style="margin-top:.35rem;">라벨 <code>' + norm + '</code> → '
        + '<a href="' + post.url + '">' + escapeHtml(post.title) + '</a></div>'
        + '</div>'
      );
    } else {
      // 입력이 맞는데도 없으면, 타이핑 오류 가능성 제안
      const prefix = norm.slice(0, 10);
      const candidates = [];
      for (const [lab, p] of labelMap) {
        if (lab.startsWith(prefix)) { candidates.push({ lab, p }); if (candidates.length >= 5) break; }
      }
      let html = '<p class="fail">일치하는 포스트를 찾지 못했습니다.</p>';
      if (candidates.length) {
        html += '<div class="suggestions">비슷한 라벨 후보:<ul style="margin:.25rem 0 0 .9rem;">'
          + candidates.map(c => '<li><code>'+c.lab+'</code> → <a href="'+c.p.url+'">'+escapeHtml(c.p.title)+'</a></li>').join('')
          + '</ul></div>';
      }
      setResult(html);
    }
  }

  // 6) 바인딩
  $btn.addEventListener('click', lookup);
  $input.addEventListener('keydown', function(e){
    if (e.key === 'Enter') { e.preventDefault(); lookup(); }
  });

  // 7) ?label= 지원
  (function autoFromQuery(){
    const u = new URL(location.href);
    const q = u.searchParams.get('label');
    if (q) { $input.value = q; lookup(); }
  })();
})();
</script>
