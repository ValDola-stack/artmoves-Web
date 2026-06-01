# artmoves-web

**The marketing website for ArtMoves** — a boutique fine art services house in Miami, founded 1987.

Live at: [wemove.art](https://wemove.art)

---

## What this is

A single-file, static HTML marketing site for ArtMoves. Six pages bundled into one file with an in-page route switcher: Home, Fine Art Handling Services, Concierge Collection Management, Fairs, Get a Quote, and About.

Generated from a structured design prompt fed to Claude Design (claude.ai). Brand-locked to the ArtMoves visual system: turquoise `#2bc9c4`, ink `#0a0a0a`, bone `#fafaf7`, Inter + Playfair Display typography, `»»` double-chevron motif.

## What this is NOT

This is **NOT** `WeMove.Art` the application. That lives in a separate repo at [`WeMoveArt_OS`](https://github.com/ValDola-stack/WeMoveArt_OS) and is deployed at `app.wemove.art`. The app is the multi-tenant operations platform that powers ArtMoves internally and is sold to partner fine art handlers, galleries, and museums (e.g. `logicart.wemove.art`).

This repo is the **public-facing brochure + lead capture surface only**.

| Repo | Surface | Stack |
|---|---|---|
| `artmoves-web` (this repo) | `wemove.art` — marketing + lead capture | Static HTML, Tailwind via CDN, Formspree for forms |
| `WeMoveArt_OS` | `app.wemove.art` + `{partner}.wemove.art` — multi-tenant operations platform | React + Supabase + Vercel (via Lovable) |

## Stack

- **Single HTML file** with Tailwind CSS via CDN, Inter + Playfair Display from Google Fonts
- **Forms:** Formspree endpoints for Quote Request and Partner Demo intake (no backend code in this repo)
- **Hosting:** Vercel static deployment
- **Domain:** `wemove.art` (apex) + `www.wemove.art` → 301 → apex

No build step. No package manager. Open `index.html` in any browser to develop locally.

## Project structure

```
artmoves-web/
├── index.html         # The entire site — all 6 pages, in-page route switcher
├── README.md          # This file
└── .gitignore
```

## Local development

Open `index.html` in any browser. Edits are immediate — save the file, refresh.

For better DX, use a lightweight static server:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploy to Vercel

**Option 1 — Drag-and-drop (fastest):**

Go to `vercel.com/new` → drag the folder containing `index.html` → Deploy. Add `wemove.art` as a custom domain in Project Settings.

**Option 2 — Git-connected (recommended for ongoing iteration):**

```bash
# In Vercel: New Project → Import Git Repository → select ValDola-stack/artmoves-Web
# Build settings: leave defaults (Vercel auto-detects static)
# Deploy
```

Every push to `main` triggers an auto-deploy.

## DNS configuration

At the domain registrar for `wemove.art`:

- `A` record: `wemove.art` → `76.76.21.21` (Vercel anycast)
- `CNAME` record: `www.wemove.art` → `cname.vercel-dns.com`
- 301 redirect from `www` → apex configured in Vercel Project Settings → Domains
- **Do NOT touch `app.wemove.art` DNS** — that's owned by the `WeMoveArt_OS` repo's Vercel project

SSL auto-provisions via Vercel (Let's Encrypt).

## Forms

Two Formspree endpoints are wired into the HTML:

| Form | Endpoint | Notification email |
|---|---|---|
| Quote Request | `formspree.io/f/[REDACTED]` | Hello@WeMove.Art |
| Partner Demo | `formspree.io/f/[REDACTED]` | Hello@WeMove.Art |

When ready to migrate forms to Supabase-backed submission with server-side PDF generation, see the migration plan in `WeMove_ART_Build_Architecture.md` (kept in the broader project workspace, not this repo).

## Editing

This is a single HTML file. To edit:

- **Copy changes** → search for the section heading or visible text, replace in place
- **Visual changes** → edit the inline `<style>` block at the top of the file
- **Add a page** → extend the in-page route switcher pattern. Each page is a `<section data-page="name">` element controlled by the small JS router at the bottom of the file
- **Form changes** → update the `action` attribute on the `<form>` element and the JS submission handler

## Brand reference

- **Founded:** 1987, Miami
- **HQ:** 2900 NW 112th Ave, Miami, FL 33172
- **Phone:** +1 305 501 0002
- **Email:** Hello@WeMove.Art
- **Insurance:** $25M aggregate (General Liability + Fine Art Packers & Movers + Excess Liability)
- **Certifications:** ISPM-15, IPPC
- **Named clients (with permission):** Heritage · Phillips · Christie's · MOCA North Miami · The Bass · The Moore · MK Artvising · Arternative
- **Google rating:** 4.8★ across 23 reviews

## Related repos

- [`WeMoveArt_OS`](https://github.com/ValDola-stack/WeMoveArt_OS) — the operations platform (separate repo, separate deploy)

## License

Proprietary. © 1987–2026 USL Consolidators LLC d/b/a ArtMoves. All rights reserved.
