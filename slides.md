---
theme: default
title: Hướng dẫn Claude Code — Từ Chat copy-paste đến Agentic Coding
info: |
  Seminar 90-120 phút cho engineer chuyển từ Chat sang Agent.
  Design: Anthropic Claude.com — cream canvas + coral CTA + dark navy mockups.
class: 'text-left'
highlighter: shiki
lineNumbers: false
fonts:
  sans: 'Inter'
  serif: 'Cormorant Garamond'
  mono: 'JetBrains Mono'
css: unocss
mdc: true
---

<style>
  @import './styles/index.css';
</style>

<!-- SLIDE 1 — TITLE -->

<div class="slidev-layout">
  <img src="/img/anthropic-logo.svg" alt="Anthropic" style="height: 28px; margin-bottom: 12px;" />
  <span class="eyebrow">Seminar · 90-120 phút</span>
  <h1>Từ Chat copy-paste<br/>đến Agentic Coding</h1>
  <p style="font-size: 22px; margin-top: 24px; color: var(--c-body-strong);">
    Hướng dẫn Claude Code cho Engineer mới bắt đầu
  </p>
  <div style="margin-top: 48px; color: var(--c-body-strong); font-size: 18px;">
    <strong>Tuan Hung Nguyen</strong> · 15/6/2026
  </div>
  <p style="margin-top: 96px; font-style: italic; color: var(--c-muted);">
    "Coding không còn là điểm nghẽn nữa." — Spotify, Code w/ Claude London 2026
  </p>
</div>

---

<!-- SLIDE 2 — PAIN POINTS -->

<div class="slidev-layout">
    <h2>Bạn đang gặp pain point nào?</h2>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 32px; margin-top: 32px;">
    <ul>
      <li>Copy đi copy lại context giữa nhiều file</li>
      <li>Code AI sinh ra không chạy được trong môi trường thật</li>
      <li>Mất context khi làm việc nhiều file cùng lúc</li>
      <li>Không biết verify output của AI có đúng không</li>
      <li>Lặp lại cùng prompt cho mỗi task tương tự</li>
      <li>Copy code vào IDE, copy lỗi quay lại chat</li>
    </ul>
    <img src="/img/claude-code-slack.webp" alt="Claude Code multi-surface" style="width: 100%; border-radius: 12px;" />
  </div>
</div>

---

<!-- SLIDE 3 — AGENDA -->

<div class="slidev-layout">
    <h2>Agenda</h2>
  <ol style="font-size: 20px; line-height: 1.8; margin-top: 32px;">
    <li>Paradigm shift — Chat vs Agent</li>
    <li>Context là tài nguyên #1</li>
    <li>Workflow cá nhân: State → Plan → Execute → Test</li>
    <li>Superpowers skills — toolkit cho cả cycle</li>
    <li>3 Live Demo xen kẽ</li>
    <li>5 pillar Claude Code</li>
    <li>Context mgmt, MCP, Hooks</li>
    <li>Lỗi hay gặp</li>
    <li>Q&A</li>
  </ol>
</div>

---

<!-- SLIDE 4 — PARADIGM SHIFT -->

<div class="slidev-layout">
    <h2>Paradigm Shift</h2>
  <table style="margin-top: 24px;">
    <thead>
      <tr>
        <th>Chat (cách cũ)</th>
        <th>Agent (cách mới)</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Bạn copy code, dán vào chat</td><td>Bạn mô tả mục tiêu</td></tr>
      <tr><td>Mô tả vấn đề</td><td>Agent tự đọc code</td></tr>
      <tr><td>AI trả lời</td><td>Agent tự sửa file</td></tr>
      <tr><td>Copy code, dán vào IDE</td><td>Agent tự chạy test</td></tr>
      <tr><td>Chạy, báo lỗi</td><td>Agent tự debug</td></tr>
      <tr><td>Copy lỗi quay lại chat</td><td>Bạn review kết quả</td></tr>
      <tr><td><strong>Vòng lặp thủ công</strong></td><td><strong>Vòng lặp tự động</strong></td></tr>
    </tbody>
  </table>
  <p style="margin-top: 32px; font-size: 20px; color: var(--c-body-strong);">
    Bạn chuyển từ <em>người gõ phím</em> → <em>người ra quyết định và review</em>.
  </p>
</div>

---

<!-- SLIDE 5 — WHY NOW -->

<div class="slidev-layout dark">
    <h2 style="color: var(--c-on-dark);">Số liệu Code w/ Claude SF 2026</h2>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 40px;">
    <div class="feature-card" style="background-color: var(--c-surface-dark-elevated); color: var(--c-on-dark);">
      <img src="/img/stripe-logo.svg" alt="Stripe" style="height: 24px; filter: brightness(0) invert(1); opacity: 0.9; margin-bottom: 12px;" />
      <p style="color: var(--c-on-dark-soft);">10,000 dòng Scala → Java trong <strong style="color: var(--c-primary);">4 ngày</strong>. Estimate ban đầu: 10 engineer-weeks.</p>
    </div>
    <div class="feature-card" style="background-color: var(--c-surface-dark-elevated); color: var(--c-on-dark);">
      <h4 style="color: var(--c-on-dark);">Wiz</h4>
      <p style="color: var(--c-on-dark-soft);">50,000 dòng Python → Go trong <strong style="color: var(--c-primary);">20 tiếng</strong>. Estimate ban đầu: 2-3 tháng.</p>
    </div>
    <div class="feature-card" style="background-color: var(--c-surface-dark-elevated); color: var(--c-on-dark);">
      <img src="/img/rakuten-logo.svg" alt="Rakuten" style="height: 24px; filter: brightness(0) invert(1); opacity: 0.9; margin-bottom: 12px;" />
      <p style="color: var(--c-on-dark-soft);">Delivery feature 24 ngày → <strong style="color: var(--c-primary);">5 ngày</strong>.</p>
    </div>
    <div class="feature-card" style="background-color: var(--c-surface-dark-elevated); color: var(--c-on-dark);">
      <img src="/img/ramp-logo.svg" alt="Ramp" style="height: 24px; opacity: 0.9; margin-bottom: 12px;" />
      <p style="color: var(--c-on-dark-soft);">Incident investigation giảm <strong style="color: var(--c-primary);">80%</strong> thời gian.</p>
    </div>
  </div>
  <p style="margin-top: 32px; color: var(--c-on-dark-soft);">Stripe deploy Claude Code cho <strong>1,370 engineer</strong>. Anthropic nội bộ: đa số code hiện viết bởi Claude Code.</p>
</div>

---

<!-- SLIDE 6 — WHAT IS CLAUDE CODE -->

<div class="slidev-layout">
    <h2>Claude Code là gì</h2>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 48px; margin-top: 32px;">
    <div>
      <p>Coding agent của Anthropic chạy trong terminal hoặc IDE.</p>
      <ul style="margin-top: 16px;">
        <li>Đọc toàn bộ codebase, không chỉ một đoạn copy-paste</li>
        <li>Tự edit file, chạy lệnh, chạy test, fix lỗi</li>
        <li>Luôn hỏi permission — <strong>bạn vẫn control</strong></li>
        <li>3 model: Opus 4.7, Sonnet 4.6, Haiku 4.5</li>
        <li>Surface: Terminal, VS Code, JetBrains, Desktop, Web, Slack</li>
      </ul>
    </div>
    <img src="/img/claude-code-hero.jpg" alt="Claude Code product" style="width: 100%; border-radius: 12px;" />
  </div>
</div>

---

<!-- SLIDE 7 — CONTEXT IS #1 -->

<div class="slidev-layout">
    <h2>Context là tài nguyên<br/>số 1</h2>
  <div style="display: grid; grid-template-columns: 3fr 2fr; gap: 48px; margin-top: 32px;">
    <div>
      <ul>
        <li>Context window = working memory của agent</li>
        <li>Gồm mọi message, file đọc, output lệnh</li>
        <li>Performance degrade khi đầy → <strong>context rot</strong></li>
        <li>200K window: system + tools = <strong>~15K</strong> trước khi bắt đầu</li>
        <li>Thêm CLAUDE.md + MCP + skills có thể đẩy 25-40K</li>
      </ul>
      <p style="margin-top: 24px; font-style: italic; color: var(--c-body-strong);">
        "Context là tài nguyên quan trọng nhất cần quản lý." — Anthropic docs
      </p>
    </div>
    <img src="/img/claude-code-web.webp" alt="Claude Code web surface" style="width: 100%; border-radius: 12px;" />
  </div>
</div>

---

<!-- SLIDE 8 — WORKFLOW OVERVIEW -->

<div class="slidev-layout coral">
    <h2 style="color: var(--c-on-primary);">4 bước</h2>
  <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; margin-top: 48px;">
    <div style="background: var(--c-on-primary); color: var(--c-ink); padding: 24px; border-radius: var(--r-lg);">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-primary); margin-bottom: 8px;">Step 1</div>
      <h4 style="margin: 0;">State Problem</h4>
      <p style="margin-top: 8px; font-size: 14px;">Observed · Expected · Repro · Constraints</p>
    </div>
    <div style="background: var(--c-on-primary); color: var(--c-ink); padding: 24px; border-radius: var(--r-lg);">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-primary); margin-bottom: 8px;">Step 2</div>
      <h4 style="margin: 0;">Plan</h4>
      <p style="margin-top: 8px; font-size: 14px;">Plan Mode · Atomic steps · Approve</p>
    </div>
    <div style="background: var(--c-on-primary); color: var(--c-ink); padding: 24px; border-radius: var(--r-lg);">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-primary); margin-bottom: 8px;">Step 3</div>
      <h4 style="margin: 0;">Execute</h4>
      <p style="margin-top: 8px; font-size: 14px;">TDD · Commit từng step · Rewind nếu sai</p>
    </div>
    <div style="background: var(--c-on-primary); color: var(--c-ink); padding: 24px; border-radius: var(--r-lg);">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-primary); margin-bottom: 8px;">Step 4</div>
      <h4 style="margin: 0;">Test (E2E)</h4>
      <p style="margin-top: 8px; font-size: 14px;">Unit · Integration · Playwright E2E</p>
    </div>
  </div>
  <p style="margin-top: 32px; color: var(--c-on-primary); font-size: 16px;">
    Mỗi bước có <strong>superpowers skill</strong> + <strong>verification loop</strong>. Bước sai → rewind, không correct.
  </p>
</div>

---

<!-- SLIDE 9 — STATE PROBLEM -->

<div class="slidev-layout">
    <h2>State Problem</h2>
  <p style="margin-top: 16px;">Định nghĩa vấn đề rõ ràng <strong>trước</strong> khi gõ prompt.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 32px;">
    <div class="feature-card" style="border-left: 4px solid var(--c-error);">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-error); margin-bottom: 8px;">Sai · Mơ hồ</div>
      <p style="font-family: var(--font-mono); font-size: 14px;">"Fix bug đăng nhập."</p>
    </div>
    <div class="feature-card" style="border-left: 4px solid var(--c-success);">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-success); margin-bottom: 8px;">Đúng · State</div>
      <p style="font-family: var(--font-mono); font-size: 13px;">
        User click 'Đăng nhập', form submit, response 200, redirect không xảy ra.
        <br/>Expected: redirect /dashboard.
        <br/>Repro: Chrome, account x@y.com.
      </p>
    </div>
  </div>
  <p style="margin-top: 32px;"><strong>Components:</strong> Observed · Expected · Repro · Constraints.</p>
  <p style="margin-top: 8px; color: var(--c-muted); font-size: 14px;">
    Superpowers skill: <code>brainstorming</code> chạy trước khi state nếu chưa rõ.
  </p>
</div>

---

<!-- SLIDE 10 — PLAN -->

<div class="slidev-layout">
    <h2>Plan</h2>
  <p style="margin-top: 16px;">Bao giờ cũng plan trước, code sau.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 32px; margin-top: 32px;">
    <ul>
      <li><strong>Shift+Tab</strong> → Plan Mode</li>
      <li>Agent đề xuất plan có check-list từng bước</li>
      <li>Bạn review → approve hoặc rewind</li>
      <li>Atomic steps = dễ verify từng cái</li>
      <li>Sai plan = rewrite, không patch</li>
      <li>Plan > 10 phút = quay về Bước 1</li>
    </ul>
    <img src="/img/claude-code-terminal.webp" alt="Claude Code Plan Mode terminal" style="width: 100%; border-radius: 12px;" />
  </div>
  <p style="margin-top: 24px; color: var(--c-muted); font-size: 14px;">
    Superpowers: <code>using-plan-mode</code>, <code>subagent-driven-development</code> cho task lớn.
  </p>
</div>

---

<!-- SLIDE 11 — EXECUTE -->

<div class="slidev-layout dark">
    <h2 style="color: var(--c-on-dark);">Execute</h2>
  <div style="display: grid; grid-template-columns: 3fr 2fr; gap: 32px; margin-top: 24px;">
    <div>
      <p style="color: var(--c-on-dark-soft);">Thực thi theo plan, mỗi step một thay đổi atomic.</p>
      <ul style="margin-top: 16px; color: var(--c-on-dark-soft); font-size: 15px;">
        <li><strong style="color: var(--c-on-dark);">Git commit từng atomic step</strong> — checkpoint để rewind</li>
        <li><strong style="color: var(--c-on-dark);">TDD style</strong>: test trước, code sau</li>
        <li><strong style="color: var(--c-on-dark);">@-mention file</strong> thay vì bắt agent tìm</li>
        <li><strong style="color: var(--c-on-dark);">Permission từng bước</strong> — không full auto trên prod</li>
        <li>Agent stuck → bảo in giả thuyết + cách verify</li>
      </ul>
      <div style="margin-top: 20px; background: var(--c-primary); color: var(--c-on-primary); padding: 16px; border-radius: var(--r-lg); font-size: 14px;">
        <strong>Rewind > correct:</strong> Sai 2 lần → <code style="background: rgba(0,0,0,0.2);">/rewind</code> về Plan.
      </div>
    </div>
    <img src="/img/claude-code-vscode.webp" alt="Claude Code VS Code" style="width: 100%; border-radius: 12px; object-fit: cover;" />
  </div>
</div>

---

<!-- SLIDE 12 — TEST E2E -->

<div class="slidev-layout">
    <h2>Test (E2E)</h2>
  <p style="margin-top: 16px;">Không có e2e test = chưa xong, không phụ thuộc agent báo "done".</p>
  <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; margin-top: 32px;">
    <div class="feature-card">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-primary); margin-bottom: 8px;">Tầng 1</div>
      <h4 style="margin: 0;">Unit</h4>
      <p style="margin-top: 8px; font-size: 14px;">Agent chạy sau mỗi edit.</p>
    </div>
    <div class="feature-card">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-primary); margin-bottom: 8px;">Tầng 2</div>
      <h4 style="margin: 0;">Integration</h4>
      <p style="margin-top: 8px; font-size: 14px;">Giao thoa nhiều module.</p>
    </div>
    <div class="feature-card" style="background-color: var(--c-primary); color: var(--c-on-primary);">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-on-primary); margin-bottom: 8px;">Tầng 3</div>
      <h4 style="margin: 0; color: var(--c-on-primary);">E2E</h4>
      <p style="margin-top: 8px; font-size: 14px; color: var(--c-on-primary);">Playwright · Claude in Chrome · Preview MCP.</p>
    </div>
  </div>
  <p style="margin-top: 32px;"><strong>E2E flow của tôi:</strong> server local (bg) → sub-agent điều khiển browser → verify click→response→DOM → return PASS/FAIL + screenshot.</p>
  <p style="margin-top: 8px; color: var(--c-muted); font-size: 14px;">
    Superpowers: <code>e2e-testing</code>, <code>using-playwright</code>, <code>defensive-programming</code>.
  </p>
</div>

---

<!-- SLIDE 13 — SUPERPOWERS SKILLS -->

<div class="slidev-layout">
    <h2>Superpowers Skills</h2>
  <p style="margin-top: 16px;">Toolkit cho cả cycle — mở source, dùng qua <code>Skill</code> tool.</p>
  <table style="margin-top: 32px;">
    <thead><tr><th>Bước</th><th>Skill chính</th></tr></thead>
    <tbody>
      <tr><td><strong>State</strong></td><td><code>brainstorming</code></td></tr>
      <tr><td><strong>Plan</strong></td><td><code>using-plan-mode</code> · <code>subagent-driven-development</code></td></tr>
      <tr><td><strong>Execute</strong></td><td><code>test-driven-development</code> · <code>root-cause-tracing</code> · <code>verification-before-completion</code></td></tr>
      <tr><td><strong>Test</strong></td><td><code>e2e-testing</code> · <code>using-playwright</code> · <code>defensive-programming</code></td></tr>
      <tr><td><strong>Cross-cutting</strong></td><td><code>using-superpowers</code> · <code>debugging</code> · <code>condition-based-waiting</code></td></tr>
    </tbody>
  </table>
  <p style="margin-top: 24px; color: var(--c-muted); font-size: 14px;">Skills auto-load khi trigger trúng → không tốn context khi không cần.</p>
</div>

---

<!-- SLIDE 14 — DEMO 1 -->

<div class="slidev-layout coral" style="display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center;">
  <span class="badge-coral" style="background: var(--c-on-primary); color: var(--c-primary);">Live Demo</span>
  <h1 style="margin-top: 24px; color: var(--c-on-primary);">Demo 1</h1>
  <h3 style="color: var(--c-on-primary); font-size: 28px; margin-top: 16px;">Full cycle: State → Plan → Execute → Test</h3>
  <p style="margin-top: 32px; color: var(--c-on-primary); font-size: 18px;">~10-12 phút</p>
</div>

---

<!-- SLIDE 15 — PILLAR 1: CLAUDE.md -->

<div class="slidev-layout">
    <h2>CLAUDE.md</h2>
  <p style="margin-top: 16px;">File markdown ở root project, Claude tự đọc mỗi session.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 32px; margin-top: 32px;">
    <div>
      <h4>Chứa</h4>
      <ul style="margin-top: 8px;">
        <li>Architecture overview</li>
        <li>Coding conventions</li>
        <li>Commands hay dùng</li>
        <li>Gotchas</li>
      </ul>
      <h4 style="margin-top: 24px;">Quy tắc độ dài</h4>
      <ul style="margin-top: 8px;">
        <li>&lt; 500 dòng: follow consistently</li>
        <li>&gt; 1000 dòng: bị ignore dần</li>
        <li>Compliance ~80% — vẫn cần verify</li>
      </ul>
    </div>
    <div class="code-window">
      <div style="color: var(--c-muted-soft); font-size: 12px; margin-bottom: 12px;">CLAUDE.md</div>
      <div v-pre style="font-family: var(--font-mono); font-size: 12px; line-height: 1.7; color: var(--c-on-dark);"><span style="color: var(--c-muted-soft);">&#35; Project Architecture</span><br/><br/><span style="color: var(--c-muted-soft);">&#35;&#35; Conventions</span><br/>- TypeScript strict mode<br/>- Prettier · ESLint<br/>- Conventional commits<br/><br/><span style="color: var(--c-muted-soft);">&#35;&#35; Commands</span><br/>- pnpm dev<br/>- pnpm test<br/>- pnpm lint<br/><br/><span style="color: var(--c-muted-soft);">&#35;&#35; Gotchas</span><br/>- Migration order matters<br/>- Use timezone-aware dates</div>
    </div>
  </div>
</div>

---

<!-- SLIDE 16 — CLAUDE.md EVOLVES -->

<div class="slidev-layout">
    <h2>CLAUDE.md sống theo thời gian</h2>
  <ul style="margin-top: 24px;">
    <li>Claude sai → bảo: <em>"Update CLAUDE.md để lần sau không lặp lại."</em></li>
    <li>Cuối session: <em>"Bạn học được gì?"</em></li>
    <li>Save: Concept → CLAUDE.md · Convention → rules · Technical → skill file</li>
    <li><strong>Commit CLAUDE.md vào git</strong> — team chia sẻ knowledge</li>
  </ul>
  <div style="margin-top: 32px;" class="callout-coral">
    <strong>Pattern:</strong> Self-improving project memory — mỗi correction = rule mới, tích lũy theo project.
  </div>
</div>

---

<!-- SLIDE 17 — PILLAR 2: PLAN MODE -->

<div class="slidev-layout">
    <h2>Plan Mode (chi tiết)</h2>
  <div style="display: grid; grid-template-columns: 2fr 3fr; gap: 32px; margin-top: 32px;">
    <div>
      <h4>Activate</h4>
      <div style="margin-top: 12px; display: flex; gap: 8px;">
        <kbd style="padding: 8px 12px; background: var(--c-canvas); border: 1px solid var(--c-hairline); border-radius: var(--r-sm); font-family: var(--font-mono);">Shift</kbd>
        <span style="line-height: 32px;">+</span>
        <kbd style="padding: 8px 12px; background: var(--c-canvas); border: 1px solid var(--c-hairline); border-radius: var(--r-sm); font-family: var(--font-mono);">Tab</kbd>
      </div>
      <h4 style="margin-top: 24px;">Khi nào dùng</h4>
      <ul>
        <li>Multi-file task</li>
        <li>Quyết định kiến trúc</li>
        <li>Bug có > 1 nguyên nhân giả định</li>
      </ul>
    </div>
    <div class="feature-card">
      <div style="font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--c-primary); margin-bottom: 12px;">Plan output</div>
      <ol style="font-family: var(--font-mono); font-size: 13px;">
        <li>Read auth middleware config</li>
        <li>Identify JWT verify path</li>
        <li>Add JWT lib + types</li>
        <li>Write test cases (10 fixtures)</li>
        <li>Refactor middleware</li>
        <li>Run test suite, fix failures</li>
        <li>Update CLAUDE.md notes</li>
      </ol>
    </div>
  </div>
</div>

---

<!-- SLIDE 18 — REWIND > CORRECT -->

<div class="slidev-layout dark">
    <h2 style="color: var(--c-on-dark);">Rewind &gt; Correct</h2>
  <div class="callout-coral" style="margin-top: 32px;">
    "Khi agent đi sai hướng, đừng correct — hãy <strong>rewind</strong>."<br/>
    <span style="font-size: 14px;">— Boris Cherny, creator Claude Code</span>
  </div>
  <ul style="margin-top: 32px; color: var(--c-on-dark-soft);">
    <li><kbd style="background: var(--c-surface-dark-elevated); padding: 4px 10px; border-radius: var(--r-sm); color: var(--c-on-dark);">Esc Esc</kbd> hoặc <code>/rewind</code> → quay về state cũ</li>
    <li>Correct giữ failed attempt → pollute mọi turn sau</li>
    <li>Sau rewind: rephrase với info vừa học</li>
    <li><strong style="color: var(--c-on-dark);">2 lần correct fail → <code>/clear</code> + prompt mới</strong></li>
  </ul>
  <p style="margin-top: 32px; color: var(--c-on-dark-soft); font-style: italic;">
    <code>/clear</code> là bạn. Không có giải thưởng cho session dài nhất.
  </p>
</div>

---

<!-- SLIDE 19 — PILLAR 3: PERMISSIONS -->

<div class="slidev-layout">
    <h2>Permissions</h2>
  <p style="margin-top: 16px;">Bạn vẫn là người ra quyết định.</p>
  <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; margin-top: 32px;">
    <div class="feature-card">
      <h4>Hỏi mỗi lần</h4>
      <p style="margin-top: 8px; font-size: 14px;">An toàn nhất. Default.</p>
    </div>
    <div class="feature-card">
      <h4>Allow safe</h4>
      <p style="margin-top: 8px; font-size: 14px;">Whitelist command hay dùng.</p>
    </div>
    <div class="feature-card" style="background: var(--c-error); color: var(--c-on-primary);">
      <h4 style="color: var(--c-on-primary);">Full auto</h4>
      <p style="margin-top: 8px; font-size: 14px; color: var(--c-on-primary);">Chỉ sandbox / worktree.</p>
    </div>
  </div>
  <ul style="margin-top: 32px;">
    <li>Cảnh báo khi agent muốn <code>rm -rf</code></li>
    <li><code>--dangerously-skip-permissions</code> tồn tại — chỉ khi hiểu rõ rủi ro</li>
    <li>Triết lý: <strong>Trust but verify</strong></li>
  </ul>
</div>

---

<!-- SLIDE 20 — PILLAR 4: VERIFICATION LOOPS -->

<div class="slidev-layout coral">
    <h2 style="color: var(--c-on-primary);">Verification Loops</h2>
  <p style="margin-top: 16px; color: var(--c-on-primary); font-size: 22px;">
    <em>Highest-leverage practice theo Anthropic.</em>
  </p>
  <div style="margin-top: 32px; background: var(--c-on-primary); color: var(--c-ink); padding: 32px; border-radius: var(--r-lg);">
    <strong>Prompt tốt:</strong>
    <p style="margin-top: 8px; font-family: var(--font-mono); font-size: 14px;">
      "Refactor auth middleware dùng JWT. Chạy test suite cũ. Fix mọi failure trước khi báo xong."
    </p>
  </div>
  <p style="margin-top: 32px; color: var(--c-on-primary);">
    Tools: test suite · linter · bash · Claude in Chrome · Playwright. Feedback loop = <strong>2-3x quality improvement</strong>.
  </p>
  <p style="margin-top: 16px; color: var(--c-on-primary); font-style: italic;">
    Không có verification loop = bạn là feedback loop duy nhất.
  </p>
</div>

---

<!-- SLIDE 21 — PILLAR 5: SLASH COMMANDS -->

<div class="slidev-layout">
    <h2>Slash Commands</h2>
  <table style="margin-top: 32px; font-family: var(--font-mono);">
    <tbody>
      <tr><td><code>/init</code></td><td>Generate CLAUDE.md</td></tr>
      <tr><td><code>/clear</code></td><td>Reset context</td></tr>
      <tr><td><code>/compact</code></td><td>Nén lịch sử</td></tr>
      <tr><td><code>/context</code></td><td>Xem breakdown token</td></tr>
      <tr><td><code>/rewind</code> (2x Esc)</td><td>Quay lại state cũ</td></tr>
      <tr><td><code>/model sonnet|opus</code></td><td>Switch model</td></tr>
      <tr><td><code>/mcp</code></td><td>Quản lý MCP servers</td></tr>
      <tr><td><code>/skills</code></td><td>Quản lý skills</td></tr>
      <tr><td><code>/cost</code></td><td>Chi phí session</td></tr>
    </tbody>
  </table>
</div>

---

<!-- SLIDE 22 — DEMO 2 -->

<div class="slidev-layout coral" style="display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center;">
  <span class="badge-coral" style="background: var(--c-on-primary); color: var(--c-primary);">Live Demo</span>
  <h1 style="margin-top: 24px; color: var(--c-on-primary);">Demo 2</h1>
  <h3 style="color: var(--c-on-primary); font-size: 28px; margin-top: 16px;">Plan + Rewind</h3>
  <p style="margin-top: 32px; color: var(--c-on-primary); font-size: 18px;">~7-10 phút</p>
</div>

---

<!-- SLIDE 23 — CONTEXT MGMT + DUMB ZONE -->

<div class="slidev-layout">
    <h2>Context · Dumb Zone</h2>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 32px; margin-top: 32px;">
    <div>
      <h4>Habits</h4>
      <ul style="margin-top: 8px;">
        <li>Glance token % trước mỗi task</li>
        <li><code>/context</code> xem breakdown</li>
        <li>Memory &gt; 15% → prune CLAUDE.md</li>
        <li><strong>Compact ở 40-50%</strong>, không đợi 95%</li>
        <li><code>/clear</code> khi sang task khác hẳn</li>
      </ul>
    </div>
    <div>
      <h4>Dumb Zone</h4>
      <table style="margin-top: 8px;">
        <thead><tr><th>Window</th><th>Dumb zone</th></tr></thead>
        <tbody>
          <tr><td>200K</td><td>60-150K</td></tr>
          <tr><td>1M</td><td>300-400K</td></tr>
        </tbody>
      </table>
      <p style="margin-top: 12px; font-size: 14px;">
        <strong>Newbie:</strong> &lt; 40% · <strong>Experienced:</strong> &lt; 30%
      </p>
      <p style="margin-top: 12px; font-size: 14px; color: var(--c-muted);">
        Dấu hiệu: gợi ý lại solution đã reject · quên rule · edit file không tồn tại.
      </p>
    </div>
  </div>
</div>

---

<!-- SLIDE 24 — MCP -->

<div class="slidev-layout">
    <h2>MCP — Model Context Protocol</h2>
  <p style="margin-top: 16px;">Giao thức kết nối tools ngoài.</p>
  <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-top: 32px;">
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;"><img src="https://cdn.simpleicons.org/github/141413" alt="" style="height: 16px; width: 16px;" />GitHub</div>
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;"><img src="https://cdn.simpleicons.org/postgresql/141413" alt="" style="height: 16px; width: 16px;" />Postgres</div>
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;">💬 Slack</div>
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;"><img src="https://cdn.simpleicons.org/linear/141413" alt="" style="height: 16px; width: 16px;" />Linear</div>
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;"><img src="https://cdn.simpleicons.org/jira/141413" alt="" style="height: 16px; width: 16px;" />Jira</div>
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;"><img src="https://cdn.simpleicons.org/sentry/141413" alt="" style="height: 16px; width: 16px;" />Sentry</div>
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;"><img src="https://cdn.simpleicons.org/figma/141413" alt="" style="height: 16px; width: 16px;" />Figma</div>
    <div class="badge-pill" style="display: flex; align-items: center; justify-content: center; gap: 8px; padding: 12px;">▶ Playwright</div>
  </div>
  <ul style="margin-top: 32px;">
    <li>Mỗi server ăn 5-10K tokens schema</li>
    <li>Tool Search auto-enable khi MCP &gt; 10% context</li>
    <li>Bắt đầu 1-2 server đơn giản</li>
  </ul>
</div>

---

<!-- SLIDE 25 — SKILLS + HOOKS -->

<div class="slidev-layout">
    <h2>Skills · Sub-agents · Hooks</h2>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 32px;">
    <div class="feature-card">
      <h4>Skills</h4>
      <ul style="margin-top: 8px; font-size: 14px;">
        <li>Folder hướng dẫn chuyên biệt, auto-load khi trigger</li>
        <li>Chia nhỏ 1 skill = 1 mục đích</li>
        <li>Superpowers ecosystem = source có sẵn</li>
      </ul>
    </div>
    <div class="feature-card">
      <h4>Sub-agents</h4>
      <ul style="margin-top: 8px; font-size: 14px;">
        <li>Spawn agent con, context riêng</li>
        <li>Chỉ return kết quả cuối</li>
        <li>Search codebase: 200 tokens vs grep 40K</li>
      </ul>
    </div>
  </div>
  <h4 style="margin-top: 32px;">Hooks vs CLAUDE.md</h4>
  <table style="margin-top: 12px;">
    <thead><tr><th></th><th>CLAUDE.md</th><th>Hooks</th></tr></thead>
    <tbody>
      <tr><td>Compliance</td><td>~80%</td><td>100%</td></tr>
      <tr><td>Type</td><td>Advisory</td><td>Deterministic</td></tr>
    </tbody>
  </table>
  <p style="margin-top: 16px; font-size: 14px;">Phải chạy MỖI LẦN → Hook. Guidance → CLAUDE.md.</p>
</div>

---

<!-- SLIDE 26 — DEMO 3 -->

<div class="slidev-layout coral" style="display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center;">
  <span class="badge-coral" style="background: var(--c-on-primary); color: var(--c-primary);">Live Demo</span>
  <h1 style="margin-top: 24px; color: var(--c-on-primary);">Demo 3</h1>
  <h3 style="color: var(--c-on-primary); font-size: 28px; margin-top: 16px;">Debug + E2E Test</h3>
  <p style="margin-top: 32px; color: var(--c-on-primary); font-size: 18px;">~10 phút</p>
</div>

---

<!-- SLIDE 27 — MISTAKES 1/2 -->

<div class="slidev-layout">
    <h2>Workflow + Context</h2>
  <ol style="margin-top: 24px; font-size: 16px;">
    <li><strong>Task mơ hồ</strong> — "Fix bug login" → agent đoán. State observed/expected/repro/constraints.</li>
    <li><strong>Skip Plan Mode</strong> task lớn → undo hàng loạt</li>
    <li><strong>Skip e2e test</strong> — "agent báo done" ≠ "thực sự done" (trust-then-verify gap)</li>
    <li><strong>Kitchen sink session</strong> — task A, hỏi B, quay lại A → context fill rác → <code>/clear</code></li>
    <li><strong>Correcting &gt; 2 lần</strong> thay vì rewind/<code>/clear</code></li>
    <li><strong>Vending machine mindset</strong> — insert prompt, receive code, done</li>
    <li><strong>CLAUDE.md &gt; 1000 dòng</strong> — rule diluted</li>
    <li><strong>Cram mọi thứ vào CLAUDE.md</strong> — procedure nên đẩy sang skill</li>
  </ol>
</div>

---

<!-- SLIDE 28 — MISTAKES 2/2 — SECURITY -->

<div class="slidev-layout dark">
    <h2 style="color: var(--c-on-dark);">Security + Verification</h2>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 32px;">
    <div>
      <h4 style="color: var(--c-error);">Security</h4>
      <ul style="color: var(--c-on-dark-soft); font-size: 15px; margin-top: 8px;">
        <li><code>--dangerously-skip-permissions</code> trên prod</li>
        <li>API token commit vào MCP config</li>
        <li>Token overprivileged ("chỉ để test")</li>
        <li>No approval gate trước irreversible command</li>
      </ul>
    </div>
    <div>
      <h4 style="color: var(--c-warning);">Verification + Cost</h4>
      <ul style="color: var(--c-on-dark-soft); font-size: 15px; margin-top: 8px;">
        <li>Skip verification loops</li>
        <li>Merge thẳng không review diff</li>
        <li>Self-fix bug Claude gây ra (vs update docs)</li>
        <li>Opus cho mọi task (1.67x token)</li>
      </ul>
    </div>
  </div>
  <div style="margin-top: 24px; display: grid; grid-template-columns: 2fr 3fr; gap: 16px; align-items: center; background: var(--c-primary); color: var(--c-on-primary); padding: 16px; border-radius: var(--r-lg);">
    <img src="/img/toms-hardware-db-wipe.jpg" alt="Tom's Hardware DB wipe headline" style="width: 100%; border-radius: 8px;" />
    <div>
      <strong>Horror story 2026:</strong> Cursor-Opus agent xoá production DB của Pocketo trong <strong>9 giây</strong>. Backup bay theo.
      <br/><span style="font-size: 13px; opacity: 0.85;">— Tom's Hardware · The Register</span>
    </div>
  </div>
</div>

---

<!-- SLIDE 29 — WHEN YES / WHEN NO -->

<div class="slidev-layout">
    <h2>Khi nào nên / không nên</h2>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 32px;">
    <div class="feature-card" style="border-top: 4px solid var(--c-success);">
      <h4 style="color: var(--c-success);">Nên</h4>
      <ul style="margin-top: 12px; font-size: 15px;">
        <li>Multi-file refactor</li>
        <li>Feature có spec rõ</li>
        <li>Debug bug khó nhiều file</li>
        <li>Viết test cho legacy</li>
        <li>Migrate code (Scala→Java, Python→Go)</li>
        <li>Onboarding codebase mới</li>
        <li>CI/CD fix test pipeline</li>
      </ul>
    </div>
    <div class="feature-card" style="border-top: 4px solid var(--c-error);">
      <h4 style="color: var(--c-error);">Không nên</h4>
      <ul style="margin-top: 12px; font-size: 15px;">
        <li>Edit 1-2 dòng đơn giản</li>
        <li>Requirement chưa rõ</li>
        <li>Code security-critical</li>
        <li>Bạn không hiểu domain</li>
        <li>Task creative thuần</li>
        <li>Context đã trong dumb zone</li>
        <li>Naming convention quan trọng</li>
      </ul>
    </div>
  </div>
</div>

---

<!-- SLIDE 30 — REVIEW -->

<div class="slidev-layout">
    <h2>Review output của agent</h2>
  <ul style="margin-top: 32px; font-size: 16px;">
    <li>☐ Đọc full diff trước accept</li>
    <li>☐ Chạy test cũ + test mới</li>
    <li>☐ Agent có xóa code nào không lý do?</li>
    <li>☐ Edge cases có xử lý?</li>
    <li>☐ E2E verify behavior trên UI thật?</li>
    <li>☐ <code>git diff</code> lần cuối trước commit</li>
  </ul>
  <div class="callout-coral" style="margin-top: 32px; padding: 32px;">
    <strong>Quy tắc vàng:</strong> Không hiểu code agent viết → <strong>ĐỪNG COMMIT.</strong>
  </div>
</div>

---

<!-- SLIDE 31 — RECAP -->

<div class="slidev-layout">
    <h2>5 điều nhớ mang về</h2>
  <div style="display: grid; grid-template-columns: repeat(5, 1fr); gap: 12px; margin-top: 32px;">
    <div class="feature-card" style="padding: 16px;">
      <div style="font-size: 28px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">1</div>
      <h4 style="margin-top: 8px; font-size: 15px;">Workflow 4 bước</h4>
      <p style="margin-top: 6px; font-size: 12px;">State → Plan → Execute → Test (e2e)</p>
    </div>
    <div class="feature-card" style="padding: 16px;">
      <div style="font-size: 28px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">2</div>
      <h4 style="margin-top: 8px; font-size: 15px;">Superpowers</h4>
      <p style="margin-top: 6px; font-size: 12px;">Mỗi bước có skill — không tự code lại</p>
    </div>
    <div class="feature-card" style="padding: 16px;">
      <div style="font-size: 28px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">3</div>
      <h4 style="margin-top: 8px; font-size: 15px;">Context #1</h4>
      <p style="margin-top: 6px; font-size: 12px;">Nhìn token %, <code>/clear</code> không tiếc</p>
    </div>
    <div class="feature-card" style="padding: 16px;">
      <div style="font-size: 28px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">4</div>
      <h4 style="margin-top: 8px; font-size: 15px;">Rewind > Correct</h4>
      <p style="margin-top: 6px; font-size: 12px;">Double-Esc khi agent sai</p>
    </div>
    <div class="feature-card" style="padding: 16px; background: var(--c-primary); color: var(--c-on-primary);">
      <div style="font-size: 28px; font-family: var(--font-display); line-height: 1;">5</div>
      <h4 style="margin-top: 8px; font-size: 15px; color: var(--c-on-primary);">Verification + e2e</h4>
      <p style="margin-top: 6px; font-size: 12px; color: var(--c-on-primary);">Highest-leverage practice</p>
    </div>
  </div>
</div>

---

<!-- SLIDE 32 — Q&A -->

<div class="slidev-layout coral" style="display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center;">
  <img src="/img/anthropic-logo.svg" alt="Anthropic" style="height: 32px; filter: brightness(0) invert(1);" />
  <h1 style="color: var(--c-on-primary); margin-top: 24px;">Q&A</h1>
  <p style="color: var(--c-on-primary); font-size: 22px; margin-top: 24px; max-width: 800px;">
    Use case bạn đang nghĩ tới? Pain point nào trong daily work?
  </p>
  <p style="color: var(--c-on-primary); font-size: 16px; margin-top: 48px; font-style: italic; max-width: 800px;">
    "Coding không còn là điểm nghẽn. Điểm nghẽn = khả năng orchestrate agent."<br/>— Spotify
  </p>
  <h2 style="color: var(--c-on-primary); margin-top: 64px;">Cảm ơn</h2>
</div>
