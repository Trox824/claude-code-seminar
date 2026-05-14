# Image Manifest — Seminar Slides

Image type per slide + suggested source. Place images at `tasks/slides/public/img/<slug>.{png,jpg,svg}`.

Naming convention: `slide-<NN>-<slug>.{ext}`

Sources legend:
- **A** = Anthropic CDN (anthropic.com/claude.com static assets)
- **U** = Undraw.co (line-art illustrations, recolor to coral/cream)
- **C** = Custom SVG diagram (build inline)
- **S** = Screenshot (presenter captures from Claude Code terminal)
- **N** = News headline screenshot (Tom's Hardware etc — public)
- **L** = Logo (brand asset, fair use small-scale)

| # | Slide | Image | Type | Source |
|---|-------|-------|------|--------|
| 1 | TITLE | Anthropic spike-mark + "Claude Code" wordmark, large hero | A | claude.com/code press kit |
| 2 | Pain points | Line-art: dev tangled in copy-paste loops, coral strokes on cream | U/C | Undraw "frustrated" recolored |
| 3 | Agenda | (text only) | — | — |
| 4 | Paradigm shift | Side-by-side flow diagram CHAT vs AGENT | C | Custom SVG (2-column flow) |
| 5 | Why now | Logos: Stripe, Wiz, Rakuten, Ramp, Anthropic (greyscale row) | L | Company press kits |
| 6 | What is Claude Code | Dark code-window mockup of `claude` prompt | S | Terminal screenshot |
| 7 | Context = #1 | Diagram: desk-with-clutter analogy (cream desk, items piling) | U/C | Custom SVG |
| 8 | Workflow 4 steps | Custom flowchart: State → Plan → Exec → Test, with rewind loop | C | Inline SVG |
| 9 | State Problem | Mock prompt card showing bad vs good prompt | C | Inline component |
| 10 | Plan | Screenshot of Plan Mode output in Claude Code | S | Terminal capture |
| 11 | Execute | Code-window with diff highlights (coral additions, ink deletions) | S/C | Terminal capture |
| 12 | Test (E2E) | Playwright trace viewer screenshot + browser thumbnail | S | Playwright report |
| 13 | Superpowers skills | Folder-tree visual of skills/ directory | C | Inline SVG/code |
| 14 | DEMO 1 | (live, no static image — use "DEMO" coral badge as title art) | — | Coral badge |
| 15 | CLAUDE.md | Markdown file mockup on cream surface | C | Inline rendered MD |
| 16 | CLAUDE.md evolves | Git diff visual showing CLAUDE.md growing | S | Git log screenshot |
| 17 | Plan Mode detail | Shift+Tab keyboard keys visual + plan checklist mockup | C | Inline SVG |
| 18 | Rewind > Correct | Double-Esc keyboard visual + context-bar before/after | C | Inline SVG |
| 19 | Permissions | Permission dialog screenshot from Claude Code | S | Terminal capture |
| 20 | Verification loops | Loop diagram: prompt → exec → test → fix → prompt | C | Inline SVG |
| 21 | Slash commands | Terminal mockup showing `/clear`, `/context`, `/init` etc | C | Code-window |
| 22 | DEMO 2 | Coral DEMO badge | — | Coral badge |
| 23 | Context mgmt + Dumb zone | Token % graph (line chart 0-100%, dumb zone shaded coral) | C | SVG line chart |
| 24 | MCP | Architecture diagram: Claude Code ↔ MCP servers ↔ tools | C | Inline SVG |
| 25 | Skills + Hooks | Side-by-side comparison cards | C | Two-column layout |
| 26 | DEMO 3 | Coral DEMO badge | — | Coral badge |
| 27 | Mistakes 1/2 | Warning icon row with line-art | U | Undraw "warning" |
| 28 | Mistakes 2/2 (security) | Screenshot of Tom's Hardware headline ("9 seconds DB wipe") | N | tomshardware.com |
| 29 | When yes/no | 2-column checkmark/x layout | C | Inline component |
| 30 | Review output | Git diff visual with annotations | S | Git diff screenshot |
| 31 | Recap 5 | 5 numbered cards in grid (cream + dark mix) | C | Inline layout |
| 32 | Q&A | Cream callout card with coral spike-mark + "Cảm ơn" | C | Inline component |

## Asset acquisition checklist

Downloaded into `public/img/`:
- [x] `anthropic-logo.svg` — Wikipedia Commons (slides 1, 32)
- [x] `claude-code-hero.jpg` — Anthropic Sanity CDN (slide 6)
- [x] `stripe-logo.svg` — Wikipedia Commons (slide 5)
- [x] `rakuten-logo.svg` — Wikipedia Commons (slide 5)
- [x] `toms-hardware-db-wipe.jpg` — Tom's Hardware OG image (slide 28)
- [x] `spike-mark.svg` — alias of anthropic-logo

Still to source:
- [ ] Wiz logo (Wikipedia path missing)
- [ ] Ramp logo (Wikipedia path missing)
- [ ] Terminal screenshots: `claude` startup, Plan Mode prompt, permission dialog, slash commands, debug session
- [ ] Playwright trace viewer screenshot (for slide 12)
- [ ] Git diff visual (for slide 30 Review)
- [ ] Plan Mode checklist screenshot (slide 10, 17)

## Image recolor rules (Undraw)

Undraw illustrations → recolor via tools or download from undraw.co/colors:
- Primary: `#cc785c` (Claude coral)
- Secondary: `#141413` (ink)
- Background: `#faf9f5` (cream — match canvas)

## Fallback strategy

If image unavailable at presentation time:
- Use `.image-placeholder` CSS class (dashed cream box with "IMAGE: <description>")
- Slide still renders cleanly — text content carries the message
