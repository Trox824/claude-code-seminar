---
theme: default
title: Claude Code for Real Engineer
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
  <span class="eyebrow">Seminar · Advanced · 90-120 phút</span>
  <h1>Claude Code<br/>for Real Engineer</h1>
  <p style="font-size: 22px; margin-top: 24px; color: var(--c-body-strong);">
    Multi-subagent · beads · /loop · design.md · cross-agent skill · cost tier
  </p>
  <p style="font-size: 15px; margin-top: 8px; color: var(--c-muted);">
    Cho team đã quen Claude Code — bước tiếp theo sau workflow cơ bản
  </p>
  <div style="margin-top: 48px; color: var(--c-body-strong); font-size: 18px;">
    <strong>Tuan Hung Nguyen</strong> · 15/6/2026
  </div>
  <p style="margin-top: 96px; font-style: italic; color: var(--c-muted);">
    "Bottleneck đã dịch từ coding sang xung quanh coding." — Fiona Fung, Anthropic
  </p>
</div>

---

<!-- SLIDE 2 — PAIN POINTS (advanced) -->

<div class="slidev-layout">
  <h2>Bạn đang gặp pain point nào?</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 13px;">Team đã dùng Claude Code — pain ở level tiếp theo.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 20px;">
    <div>
      <h4 style="margin: 0; font-size: 14px; color: var(--c-primary);">Workflow + Context</h4>
      <ul style="margin-top: 6px; font-size: 14px;">
        <li>Code AI sinh ra không chạy được trong môi trường thật</li>
        <li>Không biết verify output của AI có đúng không</li>
        <li>Mất context khi làm việc nhiều file cùng lúc</li>
        <li>Lặp lại cùng prompt cho mỗi task tương tự</li>
        <li>Agent báo "done" — thực chất chưa done</li>
        <li>Context đầy rác giữa session — quên rule, sai file</li>
      </ul>
    </div>
    <div>
      <h4 style="margin: 0; font-size: 14px; color: var(--c-primary);">Tooling + Scale</h4>
      <ul style="margin-top: 6px; font-size: 14px;">
        <li>CLAUDE.md 500+ dòng nhưng agent vẫn quên rule</li>
        <li>Không biết khi nào fan-out sub-agent</li>
        <li>Task dài 3+ ngày — agent mất state, lặp công việc</li>
        <li>Token cost tăng, quality giảm với Opus everywhere</li>
        <li>Skill chồng chéo, không rõ <em>khi nào</em> dùng cái nào</li>
        <li>Skip Plan Mode → undo hàng loạt commit</li>
      </ul>
    </div>
  </div>
  <div style="margin-top: 20px; background: var(--c-primary); color: var(--c-on-primary); border-radius: var(--r-sm); padding: 12px 16px; text-align: center; font-weight: 600; font-size: 14px;">
    Hôm nay: workflow nâng cao · multi-subagent · beads · /loop · design.md · /caveman · cross-agent skill
  </div>
</div>

---

<!-- SLIDE 3 — AGENDA -->

<div class="slidev-layout">
    <h2>Agenda</h2>
  <ol style="font-size: 18px; line-height: 1.7; margin-top: 24px;">
    <li>Context #1 + workflow State → Plan → Execute → Test</li>
    <li>Superpowers skills toolkit</li>
    <li>Live Demo: full cycle + Plan + Rewind</li>
    <li>CLAUDE.md + auto memory · Plan Mode · Rewind · Verification</li>
    <li>Context mgmt · Dumb Zone · MCP · Skills/Sub-agents/Hooks</li>
    <li><strong>Advanced:</strong> multi-subagent · beads · /loop · /simplify · design.md · /caveman · cross-agent skills · feature factory</li>
    <li>Live Demo: debug + E2E</li>
    <li>Mistakes · security · review · takeaways · Q&A</li>
  </ol>
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
    <div style="background: #181715; color: #f0eee6; border-radius: 12px; padding: 18px 20px; font-family: var(--font-mono); font-size: 12px; line-height: 1.6; align-self: center;">
      <div style="color: #cc785c;">$ /context</div>
      <div style="margin-top: 8px; opacity: 0.85;">Context window: <strong style="color: #fff;">200K</strong></div>
      <div style="margin-top: 12px; display: grid; grid-template-columns: 1fr auto; gap: 4px 12px;">
        <span>System prompt</span><span style="color: #b8b3a0;">2.6K · 1.3%</span>
        <span>System tools</span><span style="color: #b8b3a0;">17.6K · 8.8%</span>
        <span>MCP tools</span><span style="color: #b8b3a0;">0.9K · 0.5%</span>
        <span>Memory (CLAUDE.md)</span><span style="color: #b8b3a0;">0.3K · 0.2%</span>
        <span>Skills</span><span style="color: #b8b3a0;">0.1K · 0.0%</span>
        <span>Messages</span><span style="color: #b8b3a0;">30.5K · 15.3%</span>
        <span style="color: #cc785c;">Free space</span><span style="color: #cc785c;">114K · 57.0%</span>
        <span style="opacity: 0.6;">Autocompact buffer</span><span style="opacity: 0.6;">33K · 16.5%</span>
      </div>
      <div style="margin-top: 12px; height: 8px; border-radius: 4px; overflow: hidden; display: flex;">
        <div style="width: 8.8%; background: #6c7a89;"></div>
        <div style="width: 15.3%; background: #b8b3a0;"></div>
        <div style="width: 57%; background: #cc785c;"></div>
        <div style="width: 16.5%; background: #3a3833;"></div>
      </div>
    </div>
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

<!-- SLIDE 9 — STATE + PLAN -->

<div class="slidev-layout">
  <h2>State + Plan</h2>
  <p style="margin-top: 8px; color: var(--c-muted); font-size: 13px;">Bước 1-2 — define vấn đề rồi mới plan, không gõ prompt mơ hồ.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 16px;">
    <div>
      <div class="feature-card" style="border-left: 4px solid var(--c-error); padding: 10px 12px;">
        <div style="font-size: 11px; letter-spacing: 1.2px; text-transform: uppercase; color: var(--c-error);">Sai</div>
        <p style="font-family: var(--font-mono); font-size: 12px; margin: 4px 0 0;">"Fix bug đăng nhập."</p>
      </div>
      <div class="feature-card" style="border-left: 4px solid var(--c-success); margin-top: 8px; padding: 10px 12px;">
        <div style="font-size: 11px; letter-spacing: 1.2px; text-transform: uppercase; color: var(--c-success);">Đúng · Observed/Expected/Repro/Constraints</div>
        <p style="font-family: var(--font-mono); font-size: 11px; margin: 4px 0 0;">
          Click 'Đăng nhập' → 200 nhưng không redirect. Expected: /dashboard. Repro: Chrome, x@y.com.
        </p>
      </div>
      <ul style="margin-top: 10px; font-size: 13px;">
        <li><strong>Shift+Tab</strong> → Plan Mode trước khi code</li>
        <li>Atomic steps · review · approve hoặc rewind</li>
        <li>Plan &gt; 10 phút → quay lại State</li>
      </ul>
      <p style="margin-top: 6px; color: var(--c-muted); font-size: 11px;">Skills: <code>brainstorming</code>, <code>using-plan-mode</code>, <code>writing-plans</code>.</p>
    </div>
    <div style="background: #181715; color: #f0eee6; border-radius: 12px; padding: 14px 16px; font-family: var(--font-mono); font-size: 11px; line-height: 1.5; align-self: center;">
      <div style="display: flex; gap: 6px; margin-bottom: 8px;">
        <span style="background: #cc785c; color: #fff; padding: 2px 8px; border-radius: 4px; font-size: 10px; font-weight: 600;">⏸ PLAN MODE</span>
        <span style="opacity: 0.5; font-size: 10px;">Shift+Tab</span>
      </div>
      <div style="color: #cc785c;">&gt; Refactor auth → OAuth</div>
      <div style="margin-top: 8px; opacity: 0.85;">5 atomic steps:</div>
      <div style="margin-top: 4px;">
        <div>☐ Extract <span style="color: #f0c674;">verifyToken()</span></div>
        <div>☐ Add <span style="color: #f0c674;">OAuthStrategy</span></div>
        <div>☐ Google + GitHub providers</div>
        <div>☐ Wire <span style="color: #f0c674;">/login</span> route</div>
        <div>☐ Integration tests</div>
      </div>
      <div style="margin-top: 10px; opacity: 0.7; font-size: 10px;"><span style="background: #3a3833; padding: 1px 5px; border-radius: 3px;">Enter</span> approve · <span style="background: #3a3833; padding: 1px 5px; border-radius: 3px;">Esc</span> rewind</div>
    </div>
  </div>
</div>

---

<!-- SLIDE 10 — EXECUTE + TEST -->

<div class="slidev-layout dark">
  <h2 style="color: var(--c-on-dark);">Execute + Test</h2>
  <p style="margin-top: 8px; color: var(--c-on-dark-soft); font-size: 13px;">Bước 3-4 — atomic commits + 3 tầng test, agent báo "done" ≠ thực sự done.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 16px;">
    <div>
      <h4 style="color: var(--c-on-dark); margin: 0;">Execute</h4>
      <ul style="margin-top: 8px; color: var(--c-on-dark-soft); font-size: 13px;">
        <li>Git commit từng atomic step — checkpoint rewind</li>
        <li>TDD: test trước, code sau</li>
        <li>@-mention file thay vì bắt agent tìm</li>
        <li>Permission từng bước trên prod</li>
        <li>Stuck → bảo agent in giả thuyết + cách verify</li>
      </ul>
      <div style="margin-top: 12px; background: var(--c-primary); color: var(--c-on-primary); padding: 10px 12px; border-radius: var(--r-sm); font-size: 12px;">
        <strong>Rewind &gt; correct.</strong> Sai 2 lần → <code style="background: rgba(0,0,0,0.2);">/rewind</code> về Plan.
      </div>
    </div>
    <div>
      <h4 style="color: var(--c-on-dark); margin: 0;">Test (3 tầng)</h4>
      <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 6px; margin-top: 8px;">
        <div style="background: var(--c-surface-dark-elevated); color: var(--c-on-dark); padding: 8px; border-radius: 6px;">
          <div style="font-size: 10px; color: var(--c-primary); letter-spacing: 1px;">T1</div>
          <strong style="font-size: 13px;">Unit</strong>
          <p style="font-size: 11px; margin: 2px 0 0; color: var(--c-on-dark-soft);">Sau mỗi edit</p>
        </div>
        <div style="background: var(--c-surface-dark-elevated); color: var(--c-on-dark); padding: 8px; border-radius: 6px;">
          <div style="font-size: 10px; color: var(--c-primary); letter-spacing: 1px;">T2</div>
          <strong style="font-size: 13px;">Integration</strong>
          <p style="font-size: 11px; margin: 2px 0 0; color: var(--c-on-dark-soft);">Multi-module</p>
        </div>
        <div style="background: var(--c-primary); color: var(--c-on-primary); padding: 8px; border-radius: 6px;">
          <div style="font-size: 10px; letter-spacing: 1px;">T3</div>
          <strong style="font-size: 13px;">E2E</strong>
          <p style="font-size: 11px; margin: 2px 0 0;">Playwright · Chrome MCP</p>
        </div>
      </div>
      <p style="margin-top: 10px; color: var(--c-on-dark-soft); font-size: 12px;">
        E2E flow: server local (bg) → sub-agent điều khiển browser → click→response→DOM → PASS/FAIL + screenshot.
      </p>
      <p style="margin-top: 6px; color: var(--c-muted-soft); font-size: 11px;">Skills: <code>test-driven-development</code> · <code>e2e-playwright-fix-loop</code> · <code>verification-before-completion</code>.</p>
    </div>
  </div>
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

<!-- SLIDE 14 — DEMO 1 (merged) -->

<div class="slidev-layout coral" style="display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center;">
  <span class="badge-coral" style="background: var(--c-on-primary); color: var(--c-primary);">Live Demo</span>
  <h1 style="margin-top: 24px; color: var(--c-on-primary);">Demo 1</h1>
  <h3 style="color: var(--c-on-primary); font-size: 28px; margin-top: 16px;">Full cycle + Plan + Rewind</h3>
  <p style="margin-top: 32px; color: var(--c-on-primary); font-size: 18px;">~12-15 phút</p>
</div>

---

<!-- SLIDE 16 — CLAUDE.md + AUTO MEMORY -->

<div class="slidev-layout">
    <h2>CLAUDE.md + Auto Memory</h2>
  <p style="margin-top: 8px; color: var(--c-muted); font-size: 13px;">2 hệ bộ nhớ load mỗi session — official Anthropic docs.</p>
  <div style="display: grid; grid-template-columns: 3fr 2fr; gap: 24px; margin-top: 16px;">
    <table style="font-size: 12px;">
      <thead>
        <tr><th></th><th>CLAUDE.md</th><th>Auto memory</th></tr>
      </thead>
      <tbody>
        <tr><td><strong>Ai viết</strong></td><td>Bạn</td><td>Claude</td></tr>
        <tr><td><strong>Nội dung</strong></td><td>Instructions, rules</td><td>Learnings, patterns</td></tr>
        <tr><td><strong>Scope</strong></td><td>Project · user · org</td><td>Per repo</td></tr>
        <tr><td><strong>Load</strong></td><td>Full mỗi session</td><td>First 200 lines / 25KB</td></tr>
        <tr><td><strong>Dùng cho</strong></td><td>Standards, workflow, architecture</td><td>Build cmds, debug insights</td></tr>
      </tbody>
    </table>
    <div>
      <div class="feature-card" style="padding: 12px;">
        <h4 style="font-size: 13px; margin: 0;">Khi nào add CLAUDE.md</h4>
        <ul style="margin-top: 4px; font-size: 12px; padding-left: 16px;">
          <li>Claude sai cùng lỗi lần 2</li>
          <li>Code review bắt</li>
          <li>Gõ lại cùng correction</li>
          <li>Teammate mới cần cùng context</li>
        </ul>
      </div>
      <div class="feature-card" style="padding: 12px; margin-top: 10px;">
        <h4 style="font-size: 13px; margin: 0;">Best practices</h4>
        <ul style="margin-top: 4px; font-size: 12px; padding-left: 16px;">
          <li><strong>&lt; 200 dòng</strong> / file</li>
          <li>Cụ thể: <code>"2-space indent"</code></li>
          <li><code>/init</code> · <code>/memory</code></li>
          <li>Commit vào git</li>
        </ul>
      </div>
    </div>
  </div>
</div>

---

<!-- SLIDE 16b — CLAUDE.md ANTI-PATTERNS -->

<div class="slidev-layout">
  <h2>CLAUDE.md Anti-Patterns</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">~150-200 instruction budget. Mỗi rule thừa = dilute rule quan trọng. Past line 150 mất adherence, line 250 skip cả section.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div class="feature-card" style="padding: 12px; border-left: 4px solid var(--c-error);">
      <h4 style="margin: 0; color: var(--c-error); font-size: 13px;">❌ Bloat / Vague</h4>
      <div style="margin-top: 6px; background: #fdf3ee; padding: 8px 10px; border-radius: 6px; font-family: var(--font-mono); font-size: 10px; line-height: 1.5; color: var(--c-body);">
        # Coding Standards (340 dòng)<br/>
        ## Tone<br/>
        - Be a senior engineer<br/>
        - Think step by step<br/>
        - Approach as expert<br/>
        ## Persona<br/>
        - You are pragmatic<br/>
        ## Principles<br/>
        - Write clean code<br/>
        - Follow SOLID<br/>
        - DRY<br/>
        ## Never<br/>
        - Be sloppy<br/>
        - Skip tests<br/>
        ...
      </div>
      <p style="margin-top: 6px; font-size: 11px; color: var(--c-muted);">→ Personality fluff. Claude đã tự cố làm tốt. Compete budget với rule technical thực sự cần.</p>
    </div>
    <div class="feature-card" style="padding: 12px; border-left: 4px solid var(--c-success);">
      <h4 style="margin: 0; color: var(--c-success); font-size: 13px;">✅ Specific / Constraint</h4>
      <div style="margin-top: 6px; background: #181715; color: #f0eee6; padding: 8px 10px; border-radius: 6px; font-family: var(--font-mono); font-size: 10px; line-height: 1.5;">
        # Project: payment-api (80 dòng)<br/>
        ## Commands<br/>
        - pnpm test (runs vitest)<br/>
        - pnpm db:migrate (drizzle)<br/>
        ## Gotchas<br/>
        - Stripe webhook chữ ký verify ở<br/>
        &nbsp;&nbsp;routes/webhooks/stripe.ts:42<br/>
        - Migration thứ tự matters<br/>
        - Date luôn UTC trong DB<br/>
        ## Don't<br/>
        - Modify tests trừ khi user ask<br/>
        - Touch migrations/* không hỏi
      </div>
      <p style="margin-top: 6px; font-size: 11px; color: var(--c-muted);">→ Mỗi line trả lời "Claude sẽ sai gì nếu thiếu line này?". Có thì giữ, không thì xóa.</p>
    </div>
  </div>
  <div style="margin-top: 10px; display: grid; grid-template-columns: 2fr 3fr; gap: 12px;">
    <table style="font-size: 11px;">
      <thead><tr><th>Line count</th><th>Behavior</th></tr></thead>
      <tbody>
        <tr><td>&lt; 120</td><td>High-signal sweet spot</td></tr>
        <tr><td>120-200</td><td>Budget ceiling</td></tr>
        <tr><td>200-300</td><td>Adherence drop</td></tr>
        <tr><td>&gt; 300</td><td>Skip whole sections</td></tr>
      </tbody>
    </table>
    <div style="background: var(--c-primary); color: var(--c-on-primary); padding: 10px 12px; border-radius: var(--r-sm); font-size: 11px;">
      <strong>Fix recipe:</strong>
      <ul style="margin: 4px 0 0; padding-left: 14px; line-height: 1.45;">
        <li>Xóa: tone/persona/aspiration ("be senior", "think step by step")</li>
        <li>Procedure-specific → push sang <code>Skill</code></li>
        <li>Architecture overview → giữ ngắn, link doc</li>
        <li>Sai 2 lần → bảo Claude tự update CLAUDE.md để khỏi lặp</li>
        <li>Audit định kỳ: line nào xóa cũng OK → xóa</li>
      </ul>
    </div>
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
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">3 cơ chế mở rộng Claude Code — chọn theo trigger.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 12px; margin-top: 12px;">
    <div class="feature-card" style="padding: 10px 12px;">
      <h4 style="margin: 0; font-size: 14px;">Skills</h4>
      <p style="margin: 2px 0 0; font-size: 10px; color: var(--c-muted);">Auto-load khi trigger trúng</p>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.35;">
        <li>Folder hướng dẫn chuyên biệt</li>
        <li>1 skill = 1 mục đích</li>
        <li>Superpowers ecosystem</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 10px 12px;">
      <h4 style="margin: 0; font-size: 14px;">Sub-agents</h4>
      <p style="margin: 2px 0 0; font-size: 10px; color: var(--c-muted);">Context isolated, return kết quả</p>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.35;">
        <li>Spawn agent con</li>
        <li>Chỉ return kết quả cuối</li>
        <li>Search: 200 tokens vs grep 40K</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 10px 12px; background: var(--c-primary); color: var(--c-on-primary);">
      <h4 style="margin: 0; font-size: 14px; color: var(--c-on-primary);">Hooks</h4>
      <p style="margin: 2px 0 0; font-size: 10px; color: var(--c-on-primary); opacity: 0.85;">Deterministic shell command</p>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.35; color: var(--c-on-primary);">
        <li>Pre/PostToolUse, Stop</li>
        <li>100% compliance</li>
        <li>Block + transform actions</li>
      </ul>
    </div>
  </div>
  <div style="margin-top: 12px; display: grid; grid-template-columns: 1fr 1fr; gap: 14px; align-items: start;">
    <table style="font-size: 11px; line-height: 1.3;">
      <thead><tr><th></th><th>CLAUDE.md</th><th>Hooks</th></tr></thead>
      <tbody>
        <tr><td><strong>Compliance</strong></td><td>~80%</td><td>100%</td></tr>
        <tr><td><strong>Type</strong></td><td>Advisory</td><td>Deterministic</td></tr>
        <tr><td><strong>Trigger</strong></td><td>Claude cân nhắc</td><td>Shell tự chạy</td></tr>
      </tbody>
    </table>
    <div>
      <p style="font-size: 12px; margin: 0;"><strong>Decision rule:</strong></p>
      <ul style="margin: 4px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.4;">
        <li>Chạy <strong>MỖI LẦN</strong> không ngoại lệ → <strong>Hook</strong></li>
        <li>Guidance Claude cân nhắc → <strong>CLAUDE.md</strong></li>
        <li>Task-specific procedure → <strong>Skill</strong></li>
        <li>Heavy work cần context riêng → <strong>Sub-agent</strong></li>
      </ul>
    </div>
  </div>
</div>

---

<!-- SLIDE A1 — MULTI-SUBAGENT ORCHESTRATION -->

<div class="slidev-layout">
  <h2>Multi-Subagent Orchestration</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Vượt qua spawn 1 agent — fan-out song song cho task lớn.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div>
      <h4 style="margin: 0; font-size: 14px;">Khi nào fan-out</h4>
      <ul style="margin-top: 6px; font-size: 12px;">
        <li>≥ 2 task <strong>độc lập</strong> không share state</li>
        <li>Search/research nhiều ngách codebase</li>
        <li>Review nhiều khía cạnh (security · perf · style)</li>
        <li>Refactor nhiều module không phụ thuộc</li>
      </ul>
      <h4 style="margin: 12px 0 0; font-size: 14px;">Pattern thực chiến</h4>
      <table style="font-size: 11px; margin-top: 4px;">
        <tbody>
          <tr><td><code>code-explorer</code></td><td>Map architecture</td></tr>
          <tr><td><code>code-architect</code></td><td>Design blueprint</td></tr>
          <tr><td><code>code-reviewer</code></td><td>Audit diff</td></tr>
          <tr><td><code>Explore</code></td><td>Quick file lookup</td></tr>
        </tbody>
      </table>
    </div>
    <div>
      <div style="background: #181715; color: #f0eee6; border-radius: 12px; padding: 12px 14px; font-family: var(--font-mono); font-size: 11px; line-height: 1.5;">
        <div style="color: #cc785c;">// 1 message, 3 tool calls song song</div>
        <div style="margin-top: 6px;">Agent(explorer, "map auth layer")</div>
        <div>Agent(explorer, "map billing layer")</div>
        <div>Agent(explorer, "map notif layer")</div>
        <div style="margin-top: 8px; color: #cc785c;">→ 3 isolated context, return tóm tắt</div>
        <div style="margin-top: 8px; opacity: 0.7;">isolation: <span style="color: #f0c674;">"worktree"</span> → git worktree riêng</div>
      </div>
      <ul style="margin-top: 10px; font-size: 12px;">
        <li>Mỗi agent context riêng — không pollute main</li>
        <li>Chỉ return kết quả cuối — search 200 token vs grep 40K</li>
        <li>Worktree isolation cho code-writing agent</li>
      </ul>
      <p style="margin-top: 6px; color: var(--c-muted); font-size: 11px;">Skills: <code>dispatching-parallel-agents</code> · <code>subagent-driven-development</code> · <code>multi-agent-orchestration</code>.</p>
    </div>
  </div>
</div>

---

<!-- SLIDE A2 — BEADS LOCAL KANBAN -->

<div class="slidev-layout">
  <h2>beads — Local Kanban cho Agent</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Memory upgrade cho coding agent — graph issue tracker chạy local, git-friendly.</p>
  <div style="display: grid; grid-template-columns: 3fr 2fr; gap: 14px; margin-top: 12px;">
    <div>
      <table style="font-family: var(--font-mono); font-size: 12px;">
        <tbody>
          <tr><td><code>bd init</code></td><td>Tạo store + AGENTS.md</td></tr>
          <tr><td><code>bd create "..." -p 0</code></td><td>Task priority 0</td></tr>
          <tr><td><code>bd ready</code></td><td>Task không bị block</td></tr>
          <tr><td><code>bd update &lt;id&gt; --claim</code></td><td>Agent claim atomic</td></tr>
          <tr><td><code>bd show &lt;id&gt;</code></td><td>Detail + audit trail</td></tr>
          <tr><td><code>bd close &lt;id&gt; "msg"</code></td><td>Hoàn thành</td></tr>
          <tr><td><code>bd remember "..."</code></td><td>Lưu insight, bd prime inject</td></tr>
          <tr><td><code>bd ... --json</code></td><td>Parse cho agent</td></tr>
        </tbody>
      </table>
      <p style="margin-top: 8px; font-size: 12px;">
        Dependency graph: <code>relates_to</code> · <code>duplicates</code> · <code>supersedes</code> · <code>replies_to</code>. Hash ID <code>bd-a1b2</code> tránh merge conflict.
      </p>
    </div>
    <div>
      <div class="feature-card" style="padding: 10px 12px;">
        <h4 style="margin: 0; font-size: 13px;">Vs TodoWrite / Linear</h4>
        <table style="font-size: 11px; margin-top: 4px;">
          <tbody>
            <tr><td>TodoWrite</td><td>Session-scoped</td></tr>
            <tr><td>beads</td><td>Repo-scoped, git diff</td></tr>
            <tr><td>Linear/Jira</td><td>Team-scoped, cloud</td></tr>
          </tbody>
        </table>
      </div>
      <div style="margin-top: 8px; background: var(--c-primary); color: var(--c-on-primary); padding: 10px 12px; border-radius: var(--r-sm); font-size: 12px;">
        <strong>Use case:</strong> Human file 20 issue → agent <code>bd ready</code> pick task → close khi PR merge. Long-horizon work không mất context.
      </div>
      <p style="margin-top: 6px; color: var(--c-muted); font-size: 11px;">Install: <code>curl -fsSL .../install.sh | bash</code> · github.com/steveyegge/beads</p>
    </div>
  </div>
</div>

---

<!-- SLIDE A3 — /loop + /simplify -->

<div class="slidev-layout">
  <h2>/loop · /simplify</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">2 slash command bị bỏ quên — autonomy + code quality.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div class="feature-card" style="padding: 12px;">
      <h4 style="margin: 0;">/loop</h4>
      <p style="margin: 4px 0 0; font-size: 12px; color: var(--c-muted);">Chạy prompt theo interval, hoặc để model tự pace.</p>
      <div style="margin-top: 8px; background: #181715; color: #f0eee6; border-radius: 8px; padding: 10px 12px; font-family: var(--font-mono); font-size: 11px; line-height: 1.5;">
        <div style="color: #cc785c;"># Fixed interval</div>
        <div>/loop 5m /check-deploy</div>
        <div style="margin-top: 6px; color: #cc785c;"># Dynamic — model tự chọn delay</div>
        <div>/loop poll PR cho đến khi merge</div>
        <div style="margin-top: 6px; color: #cc785c;"># Autonomous loop</div>
        <div>/loop /babysit-prs</div>
      </div>
      <ul style="margin-top: 8px; font-size: 12px;">
        <li>Poll deploy / CI / PR</li>
        <li>Cron-style scheduled work</li>
        <li>Pair với hook để full autonomy</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 12px; background: var(--c-primary); color: var(--c-on-primary);">
      <h4 style="margin: 0; color: var(--c-on-primary);">/simplify</h4>
      <p style="margin: 4px 0 0; font-size: 12px; opacity: 0.85;">Review changed code → reuse, quality, efficiency → fix.</p>
      <ul style="margin-top: 8px; font-size: 12px;">
        <li>Phát hiện duplicate logic, abstraction thiếu</li>
        <li>Bắt over-engineering / dead code</li>
        <li>Auto-fix issue tìm được</li>
        <li>Chạy <strong>trước commit</strong> hoặc trước PR</li>
      </ul>
      <div style="margin-top: 10px; background: rgba(0,0,0,0.2); padding: 8px 10px; border-radius: 6px; font-family: var(--font-mono); font-size: 11px;">
        $ /simplify<br/>→ scan diff → report → apply fix
      </div>
    </div>
  </div>
</div>

---

<!-- SLIDE A4 — DESIGN.md / Warp -->

<div class="slidev-layout">
  <h2>design.md — CLAUDE.md cho UI</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Google DESIGN.md spec — agent đọc trước khi viết frontend.</p>
  <div style="display: grid; grid-template-columns: 3fr 2fr; gap: 14px; margin-top: 12px;">
    <div>
      <ul style="font-size: 13px;">
        <li><strong>Vấn đề:</strong> agent sinh UI "AI generic" — Tailwind gradient, blue-500, rounded card</li>
        <li><strong>Giải pháp:</strong> design.md = tokens · components · voice · do/don't, cụ thể cho brand</li>
        <li><strong>Setup:</strong> <code>npx getdesign@latest add warp</code></li>
        <li><strong>Catalog:</strong> 71 systems — Vercel, Stripe, Figma, Notion, Linear, Apple, Spotify, Airbnb</li>
        <li><strong>Use:</strong> "Use design.md/warp khi viết landing page" — agent reference tokens chính xác</li>
      </ul>
      <p style="margin-top: 10px; font-size: 12px;">
        <strong>Warp example:</strong> dark IDE-like block UI · terminal · developer tools. Skill <code>frontend-design</code> pair sẵn.
      </p>
    </div>
    <div class="code-window" style="padding: 12px 14px;">
      <div style="color: var(--c-muted-soft); font-size: 11px; margin-bottom: 8px;">design.md (snippet)</div>
      <div v-pre style="font-family: var(--font-mono); font-size: 11px; line-height: 1.5; color: var(--c-on-dark);"><span style="color: var(--c-muted-soft);">## Tokens</span><br/>bg: #1a1b1e<br/>accent: #af5fff<br/>radius-sm: 4px<br/><br/><span style="color: var(--c-muted-soft);">## Voice</span><br/>- Terse, technical<br/>- No marketing fluff<br/><br/><span style="color: var(--c-muted-soft);">## Don't</span><br/>- gradient backgrounds<br/>- generic SaaS hero</div>
    </div>
  </div>
</div>

---

<!-- SLIDE A5 — /caveman SKILL -->

<div class="slidev-layout">
  <h2>/caveman — Compress Token Mode</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Drop article/filler ~75% token cut · technical accuracy giữ nguyên.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div>
      <table style="font-size: 12px;">
        <thead><tr><th>Level</th><th>Cắt gì</th></tr></thead>
        <tbody>
          <tr><td><code>lite</code></td><td>Filler thôi</td></tr>
          <tr><td><code>full</code> (default)</td><td>Article + fragment OK</td></tr>
          <tr><td><code>ultra</code></td><td>Tối đa, telegram style</td></tr>
        </tbody>
      </table>
      <ul style="margin-top: 10px; font-size: 12px;">
        <li><strong>Giữ nguyên:</strong> code block · commit message · security warning · error message</li>
        <li><strong>Auto-clarity:</strong> destructive op, multi-step → revert normal</li>
        <li>Toggle: <code>/caveman lite|full|ultra</code> · <code>stop caveman</code></li>
        <li>Pair với <strong>Dumb Zone</strong> — context tight = caveman ON</li>
      </ul>
    </div>
    <div>
      <div class="feature-card" style="padding: 10px 12px;">
        <h4 style="margin: 0; font-size: 13px;">Before · After</h4>
        <div style="margin-top: 8px; padding: 8px; background: #fdf3ee; border-radius: 6px; font-size: 11px; line-height: 1.5;">
          <strong style="color: var(--c-error);">Normal:</strong> "Sure! I'd be happy to help. The bug you're seeing is likely caused by..."
        </div>
        <div style="margin-top: 6px; padding: 8px; background: #181715; color: #f0eee6; border-radius: 6px; font-size: 11px; line-height: 1.5;">
          <strong style="color: #cc785c;">Caveman:</strong> "Bug in auth middleware. Token check use <code style="color: #f0c674;">&lt;</code> not <code style="color: #f0c674;">&lt;=</code>. Fix:"
        </div>
      </div>
      <p style="margin-top: 8px; font-size: 12px;">
        Cũng có <code>/caveman-commit</code> và <code>/caveman-review</code> — commit message và PR review siêu nén.
      </p>
      <p style="margin-top: 4px; color: var(--c-muted); font-size: 11px;">Plugin: caveman (skill marketplace).</p>
    </div>
  </div>
</div>

---

<!-- SLIDE A6 — skills.sh + find-skills -->

<div class="slidev-layout">
  <h2>Skill Discovery</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Tìm skill phù hợp — đừng tự viết lại nếu có sẵn.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div class="feature-card" style="padding: 12px;">
      <h4 style="margin: 0; font-size: 14px;"><code>find-skills</code> skill</h4>
      <p style="margin: 4px 0 0; font-size: 12px; color: var(--c-muted);">Built-in discovery — hỏi "có skill nào làm X?" → trả về match.</p>
      <ul style="margin-top: 8px; font-size: 12px;">
        <li>Trigger: "how do I do X", "find skill for X"</li>
        <li>Browse namespace: <code>superpowers:*</code>, <code>anthropic-skills:*</code>, <code>frontend-design:*</code>, <code>caveman:*</code></li>
        <li>Install on-demand</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 12px;">
      <h4 style="margin: 0; font-size: 14px;"><code>skills.sh</code> script</h4>
      <p style="margin: 4px 0 0; font-size: 12px; color: var(--c-muted);">Shell helper — list local skill, grep description, install.</p>
      <div style="margin-top: 8px; background: #181715; color: #f0eee6; border-radius: 8px; padding: 10px 12px; font-family: var(--font-mono); font-size: 11px; line-height: 1.5;">
        <div>$ ls ~/.claude/skills/</div>
        <div style="color: #b8b3a0; margin-top: 4px;">brainstorming/ test-driven-development/ ...</div>
        <div style="margin-top: 6px;">$ skills.sh search "playwright"</div>
        <div style="color: #b8b3a0; margin-top: 4px;">→ playwright-cli, e2e-playwright-fix-loop</div>
      </div>
    </div>
  </div>
  <div style="margin-top: 12px; background: var(--c-primary); color: var(--c-on-primary); padding: 10px 14px; border-radius: var(--r-sm); font-size: 12px;">
    <strong>Rule:</strong> Task lặp lại lần 2 → tìm skill. Không có → viết với <code>skill-creator</code>. 1 skill = 1 mục đích.
  </div>
</div>

---

<!-- SLIDE A7 — CROSS-AGENT SKILL SETUP -->

<div class="slidev-layout">
  <h2>1 Skill — Nhiều Coding Agent</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Skill dùng được trên Claude Code, Copilot CLI, Gemini CLI, Codex — không lock-in.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div>
      <h4 style="margin: 0; font-size: 14px;">Priority chain</h4>
      <table style="font-size: 12px; margin-top: 6px;">
        <thead><tr><th>Priority</th><th>File</th><th>Agent</th></tr></thead>
        <tbody>
          <tr><td>1 (cao nhất)</td><td><code>CLAUDE.md</code></td><td>Claude Code</td></tr>
          <tr><td>1</td><td><code>AGENTS.md</code></td><td>Universal (Codex/Copilot)</td></tr>
          <tr><td>1</td><td><code>GEMINI.md</code></td><td>Gemini CLI</td></tr>
          <tr><td>2</td><td>Skill</td><td>Override default</td></tr>
          <tr><td>3</td><td>System prompt</td><td>Default</td></tr>
        </tbody>
      </table>
      <p style="margin-top: 8px; font-size: 12px;">
        User instruction <strong>luôn thắng</strong> — skill conflict → CLAUDE.md/AGENTS.md win.
      </p>
    </div>
    <div>
      <h4 style="margin: 0; font-size: 14px;">Cross-platform skill</h4>
      <ul style="margin-top: 6px; font-size: 12px;">
        <li>Skill viết với CC tool name (Read/Edit/Bash...)</li>
        <li>Copilot CLI: dùng <code>references/copilot-tools.md</code> map</li>
        <li>Codex: <code>references/codex-tools.md</code></li>
        <li>Gemini: auto-load via GEMINI.md</li>
        <li>Shared <code>~/.claude/skills/</code> → dùng chéo nếu folder cùng path</li>
      </ul>
      <div style="margin-top: 10px; background: var(--c-primary); color: var(--c-on-primary); padding: 10px 12px; border-radius: var(--r-sm); font-size: 12px;">
        <strong>Setup team:</strong> commit <code>CLAUDE.md</code> + <code>AGENTS.md</code> + <code>.claude/skills/</code> vào repo → mọi engineer cùng workflow.
      </div>
    </div>
  </div>
</div>

---

<!-- SLIDE A8 — AUTONOMOUS FEATURE FACTORY -->

<div class="slidev-layout dark">
  <h2 style="color: var(--c-on-dark);">Autonomous Feature Factory</h2>
  <p style="margin-top: 4px; color: var(--c-muted-soft); font-size: 12px;">Tie A1-A7: long-horizon work với minimal human-in-loop.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div>
      <ol style="color: var(--c-on-dark-soft); font-size: 13px;">
        <li><strong style="color: var(--c-on-dark);">Spec</strong> — design.md (UI) + CLAUDE.md (architecture)</li>
        <li><strong style="color: var(--c-on-dark);">Queue</strong> — <code>bd create</code> 10 issue, dependency graph</li>
        <li><strong style="color: var(--c-on-dark);">Dispatch</strong> — main agent <code>bd ready</code> → spawn 3 sub-agent song song (worktree isolated)</li>
        <li><strong style="color: var(--c-on-dark);">Verify</strong> — mỗi sub-agent chạy <code>/simplify</code> + e2e test trước khi close</li>
        <li><strong style="color: var(--c-on-dark);">Loop</strong> — <code>/loop</code> poll queue đến khi empty</li>
        <li><strong style="color: var(--c-on-dark);">Compress</strong> — <code>/caveman</code> mọi message intermediate</li>
        <li><strong style="color: var(--c-on-dark);">Review</strong> — human review PR cuối, không từng commit</li>
      </ol>
    </div>
    <div>
      <div style="background: var(--c-surface-dark-elevated); padding: 14px 16px; border-radius: 12px; font-family: var(--font-mono); font-size: 11px; line-height: 1.55; color: var(--c-on-dark);">
        <div style="color: #cc785c;">// main agent loop</div>
        <div>while bd ready --json | jq '.[]'; do</div>
        <div style="padding-left: 12px;">id = $(bd ready --json | head 1)</div>
        <div style="padding-left: 12px;">Agent({</div>
        <div style="padding-left: 24px;">subagent: "feature-dev",</div>
        <div style="padding-left: 24px;">isolation: "worktree",</div>
        <div style="padding-left: 24px;">prompt: $(bd show $id)</div>
        <div style="padding-left: 12px;">})</div>
        <div style="padding-left: 12px;">bd close $id "PR #..."</div>
        <div>done</div>
      </div>
      <div style="margin-top: 12px; background: var(--c-primary); color: var(--c-on-primary); padding: 10px 12px; border-radius: var(--r-sm); font-size: 12px;">
        <strong>Caveat:</strong> chỉ chạy với spec rõ + verification loop chắc + worktree isolation. Skip 1 cái = horror story.
      </div>
    </div>
  </div>
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

<!-- SLIDE 27 — ADVANCED ANTI-PATTERNS -->

<div class="slidev-layout">
  <h2>Advanced Anti-Patterns</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Lỗi level senior — bị trả giá bằng token, latency, hoặc bug ẩn.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 12px;">
    <div>
      <h4 style="margin: 0; font-size: 13px; color: var(--c-primary);">Sub-agent + Orchestration</h4>
      <ul style="margin-top: 4px; font-size: 12px; line-height: 1.45;">
        <li><strong>Fan-out task tuần tự</strong> — sub-agent B cần kết quả A. Token gấp 3, không nhanh hơn.</li>
        <li><strong>Spawn fresh agent thay vì SendMessage</strong> tiếp tục — mất context, làm lại research.</li>
        <li><strong>Sub-agent quên isolation: "worktree"</strong> khi viết code — 3 agent edit cùng file → race.</li>
        <li><strong>"based on findings, fix it"</strong> — push synthesis cho sub-agent thay vì tự hiểu.</li>
      </ul>
      <h4 style="margin: 10px 0 0; font-size: 13px; color: var(--c-primary);">Skill + MCP</h4>
      <ul style="margin-top: 4px; font-size: 12px; line-height: 1.45;">
        <li><strong>Skill description sai trigger</strong> — 50 skill install, không cái nào fire.</li>
        <li><strong>MCP everything</strong> — 8 server × 7K schema = 56K trước turn 1.</li>
        <li><strong>Custom skill trùng built-in</strong> — chưa <code>find-skills</code> trước khi viết.</li>
      </ul>
    </div>
    <div>
      <h4 style="margin: 0; font-size: 13px; color: var(--c-primary);">Cost + Model</h4>
      <ul style="margin-top: 4px; font-size: 12px; line-height: 1.45;">
        <li><strong>Opus mọi task</strong> — boilerplate rename = Haiku đủ. 1.67x→10x token.</li>
        <li><strong>Bỏ prompt cache</strong> — không stable prefix, hit rate &lt; 30%.</li>
        <li><strong>Sleep 300s</strong> trong loop — đúng TTL cache miss. Dùng &lt; 270s hoặc &gt; 1200s.</li>
      </ul>
      <h4 style="margin: 10px 0 0; font-size: 13px; color: var(--c-primary);">Hook + Permission</h4>
      <ul style="margin-top: 4px; font-size: 12px; line-height: 1.45;">
        <li><strong>Hook block hợp pháp</strong> — pre-commit reject mọi commit có TODO.</li>
        <li><strong>Auto-accept worktree</strong> — assume safe, agent <code>rm -rf</code> ngoài worktree.</li>
        <li><strong>AGENTS.md vs CLAUDE.md conflict</strong> — agent đoán theo file gần hơn.</li>
        <li><strong>--dangerously-skip-permissions</strong> không sandbox = horror story.</li>
      </ul>
    </div>
  </div>
</div>

---

<!-- SLIDE 28 — SECURITY + DEFENSE -->

<div class="slidev-layout dark">
  <h2 style="color: var(--c-on-dark);">Security · Defense-in-Depth</h2>
  <p style="margin-top: 4px; color: var(--c-muted-soft); font-size: 12px;">Layer nhiều lớp — không tin agent + không tin user + không tin tool.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 10px;">
    <div>
      <h4 style="color: var(--c-error); margin: 0; font-size: 13px;">Risk vectors</h4>
      <ul style="color: var(--c-on-dark-soft); font-size: 12px; margin-top: 4px; line-height: 1.45;">
        <li><code>--dangerously-skip-permissions</code> trên prod</li>
        <li>Prompt injection qua tool result (MCP, web fetch)</li>
        <li>API token overprivileged commit vào MCP config</li>
        <li>Click link trong email/PDF từ agent</li>
        <li>Irreversible cmd không gate (<code>rm -rf</code>, DROP TABLE, force-push)</li>
      </ul>
    </div>
    <div>
      <h4 style="color: var(--c-warning); margin: 0; font-size: 13px;">Defense layers</h4>
      <ul style="color: var(--c-on-dark-soft); font-size: 12px; margin-top: 4px; line-height: 1.45;">
        <li><strong>Sandbox:</strong> worktree / docker — blast radius giới hạn</li>
        <li><strong>Permission allowlist</strong> trong <code>.claude/settings.json</code></li>
        <li><strong>PreToolUse hook:</strong> block <code>rm -rf</code>, force-push, prod DB</li>
        <li><strong>Stop hook:</strong> chạy linter/secret scan trước khi user thấy</li>
        <li><strong>Subagent <code>code-reviewer</code> + <code>/security-review</code></strong> trước merge</li>
        <li>Read-only mode browser/IDE tier (computer-use tier system)</li>
      </ul>
    </div>
  </div>
  <div style="margin-top: 10px; display: grid; grid-template-columns: 1fr 2fr; gap: 12px; align-items: center; background: var(--c-primary); color: var(--c-on-primary); padding: 10px 14px; border-radius: var(--r-sm);">
    <img src="/img/toms-hardware-db-wipe.jpg" alt="Tom's Hardware DB wipe" style="width: 100%; height: 70px; object-fit: cover; border-radius: 6px;" />
    <div style="font-size: 12px;">
      <strong>Horror 2026:</strong> Cursor-Opus xoá production DB Pocketo <strong>9 giây</strong>, backup bay theo. <em>Cause: skip-permissions + no hook + no sandbox.</em>
    </div>
  </div>
</div>

---

<!-- SLIDE 29 — MODEL + COST STRATEGY -->

<div class="slidev-layout">
  <h2>Model + Cost Strategy</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Tier-up khi cần thinking, tier-down khi grind. Cache là tiền.</p>
  <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-top: 12px;">
    <div class="feature-card" style="padding: 10px 12px;">
      <h4 style="margin: 0; font-size: 13px;">Haiku 4.5</h4>
      <p style="margin: 2px 0 0; font-size: 11px; color: var(--c-muted);">~1/10 cost Opus</p>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.4;">
        <li>Rename, format, codemod</li>
        <li>File search, grep wrapper</li>
        <li>Lint fix, import sort</li>
        <li>Statusline, hook scripts</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 10px 12px;">
      <h4 style="margin: 0; font-size: 13px;">Sonnet 4.6</h4>
      <p style="margin: 2px 0 0; font-size: 11px; color: var(--c-muted);">Workhorse · default</p>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.4;">
        <li>Execute step trong plan</li>
        <li>Write test, debug đơn giản</li>
        <li>Refactor 1-3 file</li>
        <li>Most sub-agent</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 10px 12px; background: var(--c-primary); color: var(--c-on-primary);">
      <h4 style="margin: 0; font-size: 13px; color: var(--c-on-primary);">Opus 4.7</h4>
      <p style="margin: 2px 0 0; font-size: 11px; opacity: 0.85;">Thinking heavy</p>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.4;">
        <li>Plan Mode cho task lớn</li>
        <li>Root-cause bug đa file</li>
        <li>Architecture decision</li>
        <li>Multi-agent orchestrator</li>
      </ul>
    </div>
  </div>
  <div style="margin-top: 14px; display: grid; grid-template-columns: 3fr 2fr; gap: 12px;">
    <div>
      <h4 style="margin: 0; font-size: 13px;">Cache + thinking budget</h4>
      <ul style="margin-top: 4px; font-size: 12px; line-height: 1.45;">
        <li><strong>Prompt cache TTL 5 phút</strong> — stable prefix (system + CLAUDE.md + skills) hit ~90%. Skill load mid-turn = bust cache.</li>
        <li><strong>Thinking levels:</strong> <code>think</code> &lt; <code>think hard</code> &lt; <code>think harder</code> &lt; <code>ultrathink</code>. Bậc cao chỉ khi nhánh decision phức tạp.</li>
        <li><strong>Headless mode</strong> <code>claude -p "..."</code> cho CI, script — chỉ output cuối, no UI overhead.</li>
        <li><strong>Sub-agent isolation</strong> = context fresh per task → cache reuse cao hơn 1 session dài.</li>
      </ul>
    </div>
    <div style="background: #181715; color: #f0eee6; border-radius: 8px; padding: 10px 12px; font-family: var(--font-mono); font-size: 11px; line-height: 1.5;">
      <div style="color: #cc785c;"># Switch giữa session</div>
      <div>/model haiku</div>
      <div>/model sonnet</div>
      <div>/model opus</div>
      <div style="margin-top: 6px; color: #cc785c;"># Cost monitor</div>
      <div>/cost</div>
      <div style="color: #b8b3a0; font-size: 10px;">Session $2.14 · cache 87%</div>
      <div style="margin-top: 6px; color: #cc785c;"># Headless</div>
      <div>claude -p "fix lint"</div>
    </div>
  </div>
</div>

---

<!-- SLIDE 30 — ADVANCED REVIEW PIPELINE -->

<div class="slidev-layout">
  <h2>Advanced Review Pipeline</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Agent review agent — human review cuối. Mỗi layer khác nhau.</p>
  <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; margin-top: 12px;">
    <div class="feature-card" style="padding: 10px 12px;">
      <div style="font-size: 10px; color: var(--c-primary); letter-spacing: 1.2px; text-transform: uppercase;">Layer 1 · Inline</div>
      <h4 style="margin: 4px 0 0; font-size: 13px;">/simplify</h4>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.45;">
        <li>Scan diff, bắt dup logic</li>
        <li>Dead code, over-engineer</li>
        <li>Auto-fix issue</li>
        <li>Chạy trước commit</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 10px 12px;">
      <div style="font-size: 10px; color: var(--c-primary); letter-spacing: 1.2px; text-transform: uppercase;">Layer 2 · Subagent</div>
      <h4 style="margin: 4px 0 0; font-size: 13px;">code-reviewer · security-review</h4>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.45;">
        <li>Confidence-based filter — chỉ báo issue chắc</li>
        <li>Independent từ author agent</li>
        <li><code>/security-review</code> branch pending</li>
        <li>Spawn parallel với feature-dev</li>
      </ul>
    </div>
    <div class="feature-card" style="padding: 10px 12px; background: var(--c-primary); color: var(--c-on-primary);">
      <div style="font-size: 10px; letter-spacing: 1.2px; text-transform: uppercase;">Layer 3 · Cloud</div>
      <h4 style="margin: 4px 0 0; font-size: 13px; color: var(--c-on-primary);">/ultrareview</h4>
      <ul style="margin: 6px 0 0; font-size: 11px; padding-left: 14px; line-height: 1.45;">
        <li>Multi-agent cloud review</li>
        <li>Local branch hoặc PR#</li>
        <li>User-triggered, billed</li>
        <li>Before merge big change</li>
      </ul>
    </div>
  </div>
  <div style="margin-top: 12px; display: grid; grid-template-columns: 3fr 2fr; gap: 12px;">
    <div>
      <h4 style="margin: 0; font-size: 13px;">Hook-enforced gates</h4>
      <ul style="margin-top: 4px; font-size: 12px; line-height: 1.45;">
        <li><strong>PreToolUse</strong> Bash <code>git commit</code> → require diff review confirmation</li>
        <li><strong>PostToolUse</strong> Edit → auto run formatter + linter</li>
        <li><strong>Stop</strong> hook → run unit test, block "done" if red</li>
        <li><strong>Audit:</strong> agent xóa code không lý do? File ngoài scope plan?</li>
      </ul>
    </div>
    <div class="callout-coral" style="padding: 12px 14px;">
      <strong>Golden rule:</strong> Không hiểu code agent viết → <strong>ĐỪNG COMMIT.</strong><br/>
      <span style="font-size: 11px;">Review pipeline = filter, không thay người ra quyết định cuối.</span>
    </div>
  </div>
</div>

---

<!-- SLIDE 31 — ADVANCED RECAP -->

<div class="slidev-layout">
  <h2>7 điều nhớ mang về</h2>
  <p style="margin-top: 4px; color: var(--c-muted); font-size: 12px;">Cấp độ tiếp theo cho team đã quen Claude Code.</p>
  <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-top: 12px;">
    <div class="feature-card" style="padding: 12px;">
      <div style="font-size: 22px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">1</div>
      <h4 style="margin-top: 4px; font-size: 13px;">Fan-out song song</h4>
      <p style="margin-top: 4px; font-size: 11px;">1 message · nhiều Agent · worktree isolation cho task độc lập.</p>
    </div>
    <div class="feature-card" style="padding: 12px;">
      <div style="font-size: 22px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">2</div>
      <h4 style="margin-top: 4px; font-size: 13px;">beads queue</h4>
      <p style="margin-top: 4px; font-size: 11px;"><code>bd ready</code> · graph dep · long-horizon work không mất state.</p>
    </div>
    <div class="feature-card" style="padding: 12px;">
      <div style="font-size: 22px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">3</div>
      <h4 style="margin-top: 4px; font-size: 13px;">/loop + /simplify</h4>
      <p style="margin-top: 4px; font-size: 11px;">Poll autonomy + review-then-fix trước commit.</p>
    </div>
    <div class="feature-card" style="padding: 12px;">
      <div style="font-size: 22px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">4</div>
      <h4 style="margin-top: 4px; font-size: 13px;">design.md</h4>
      <p style="margin-top: 4px; font-size: 11px;">CLAUDE.md cho UI · agent dừng sinh "AI generic".</p>
    </div>
    <div class="feature-card" style="padding: 12px;">
      <div style="font-size: 22px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">5</div>
      <h4 style="margin-top: 4px; font-size: 13px;">CLAUDE.md &lt; 120 dòng</h4>
      <p style="margin-top: 4px; font-size: 11px;">Audit thường — push procedure sang Skill.</p>
    </div>
    <div class="feature-card" style="padding: 12px;">
      <div style="font-size: 22px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">6</div>
      <h4 style="margin-top: 4px; font-size: 13px;">Model tier theo task</h4>
      <p style="margin-top: 4px; font-size: 11px;">Haiku grind · Sonnet workhorse · Opus thinking.</p>
    </div>
    <div class="feature-card" style="padding: 12px; background: var(--c-primary); color: var(--c-on-primary);">
      <div style="font-size: 22px; font-family: var(--font-display); line-height: 1;">7</div>
      <h4 style="margin-top: 4px; font-size: 13px; color: var(--c-on-primary);">Defense-in-depth</h4>
      <p style="margin-top: 4px; font-size: 11px;">Sandbox + hook + reviewer agent + human gate.</p>
    </div>
    <div class="feature-card" style="padding: 12px; background: #181715; color: var(--c-on-dark);">
      <div style="font-size: 22px; font-family: var(--font-display); color: var(--c-primary); line-height: 1;">∞</div>
      <h4 style="margin-top: 4px; font-size: 13px; color: var(--c-on-dark);">find-skills first</h4>
      <p style="margin-top: 4px; font-size: 11px; color: var(--c-on-dark-soft);">Đừng tự viết — namespace <code>superpowers</code>, <code>anthropic-skills</code> đã có.</p>
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
    "Bottleneck đã dịch từ coding sang xung quanh coding."<br/>— Fiona Fung, Anthropic
  </p>
  <h2 style="color: var(--c-on-primary); margin-top: 64px;">Cảm ơn</h2>
</div>
