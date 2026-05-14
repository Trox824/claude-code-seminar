# Claude Code Seminar

Slidev deck for **"Từ Chat copy-paste đến Agentic Coding"** — Vietnamese seminar for engineers transitioning from chat-based AI coding to Claude Code agentic workflow.

Presenter: **Tuan Hung Nguyen** · 15/6/2026

## Stack

- **Slidev** — markdown-based slides, Vue-powered
- **Theme** — custom CSS tokens from `DESIGN.md` (Anthropic Claude.com design system, via `npx getdesign@latest add claude`)
- **Fonts** — Cormorant Garamond (serif display), Inter (sans body), JetBrains Mono (code)

## Local dev

```bash
npm install
npm run dev          # opens http://localhost:3030
```

## Production build (static SPA)

```bash
npm run build        # outputs dist/
npm start            # serves dist/ on $PORT (default 3000)
```

## Railway deploy

Auto-detected. Push to GitHub → connect on railway.app.

`railway.toml`:
- `buildCommand`: `npm install && npm run build`
- `startCommand`: `npm run start`

Railway sets `PORT` env automatically. `serve dist -l $PORT -s` picks it up.

## Files

| File | Purpose |
|------|---------|
| `slides.md` | 32 slides — embedded HTML/CSS, design-token-driven |
| `styles/index.css` | Design tokens (Claude cream/coral/dark) + component classes |
| `DESIGN.md` | Anthropic Claude.com design system reference |
| `image-manifest.md` | Per-slide image type + source |
| `public/img/` | Logos, hero images, headline screenshots |
| `railway.toml` | Railway deploy config |

## Design tokens cheat sheet

| Surface | Class | Use |
|---------|-------|-----|
| Cream canvas | `.slidev-layout` (default) | Body slides |
| Dark navy | `.slidev-layout.dark` | Code mockups, security, contrast slides |
| Coral | `.slidev-layout.coral` | DEMO slides, callouts, Q&A close |

Surface rhythm alternates per Anthropic pacing guide.

## Editing

Each slide = single `<div class="slidev-layout">` block between `---` separators.

CSS classes in `styles/index.css`:
- `.feature-card` — cream content card
- `.code-window` — dark code/terminal mockup
- `.callout-coral` — coral full-bleed callout
- `.badge-pill`, `.badge-coral` — pills
- `.eyebrow` — small uppercase coral label
