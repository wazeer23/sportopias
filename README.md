# Sportopias — AI-Powered Sports Journalism Platform

**Live:** [sportopias.com](https://sportopias.com)

A full-stack sports platform combining automated AI journalism, an interactive NFL GM simulator, and a 2D football practice game — built with Next.js 16, React 19, and TypeScript.

---

## What It Does

Sportopias is three products in one:

### 1. Automated Content Pipeline
An end-to-end system that discovers sports reporters, ingests news articles and tweets, selects trending topics, and generates original long-form journalism — all without manual intervention.

- **7-stage pipeline:** Discovery → Grounding → Web Scraping → Twitter Ingestion → Topic Selection → Article Generation → Publishing
- **Multi-provider LLM orchestration** across Gemini, OpenRouter, and Claude — optimized for cost ($0 for most operations)
- **Fact-checking feedback loop** — generated articles are validated against source material and regenerated if inaccuracies are found
- **Team-agnostic architecture** — change one config file and the entire pipeline works for any NFL team
- **Zod-validated LLM responses** throughout — no raw JSON parsing

### 2. NFL GM Simulator
A client-side offseason simulation where you manage an NFL franchise through the full offseason cycle.

- **6 phases:** Coaching Staff → Free Agency → NFL Draft → Roster Cuts → Trades → Season
- **Zustand state management** with 7 modular store slices and localStorage persistence
- **AI-powered scouting reports** generated via Gemini (zero cost)
- **Real data foundation** — 32 teams bootstrapped from actual rosters, contracts, and coaching staffs
- **Pure TypeScript game engine** — all logic separated from React, fully testable

### 3. Practice Mode
A 2D football practice game with custom physics, where you control the QB, call plays, and run after the catch.

- **Custom force-based physics engine** (F=ma, Euler integration) running at 60fps
- **Canvas 2D rendering** — no game framework dependencies
- **18 plays, 12 receiver routes, 5 defensive schemes**
- **Defensive AI:** Man/zone coverage with reaction delays, OL/DL block engagements
- **Ball carrier mechanics:** Juke, spin, stiff-arm, truck — probabilistic tackle system
- **Hot routes:** Pre-snap receiver route reassignment
- **Telemetry system** with headless CLI for batch simulation

---

## Technical Highlights

| Area | Details |
|------|---------|
| **Framework** | Next.js 16 (App Router), React 19, TypeScript |
| **Styling** | Tailwind CSS 4, CSS variables, responsive editorial design |
| **State** | Zustand with slice pattern, localStorage persistence |
| **Content** | MDX articles rendered with `next-mdx-remote`, JSON manifest |
| **LLM Integration** | Multi-provider (Gemini, OpenRouter, Claude), Zod schema validation |
| **Rendering** | Canvas 2D (practice), Three.js + Rapier physics (3D game mode) |
| **SEO** | Dynamic OG tags, JSON-LD schema, sitemap, robots.txt |
| **Deploy** | Vercel with automatic deployments |

---

## Architecture

```
app/                    # Next.js App Router pages
  articles/[slug]/      # Dynamic MDX article rendering
  simulator/[saveId]/   # GM simulator subpages (draft, FA, roster, etc.)
  practice/             # Full-viewport canvas game
  category/[slug]/      # Article category pages

pipeline/               # Automated content generation
  discovery/            # LLM-powered reporter/account discovery
  ingest/               # Web scraping + Twitter ingestion
  generate/             # Topic selection + article generation
  publish/              # MDX publishing + manifest updates

simulator/              # GM simulator engine + state
  engine/               # Pure TypeScript game logic
  store/                # Zustand slices (7 modules)
  components/           # Dark HUD-themed UI

practice/               # 2D practice game
  engine/               # Physics, defender AI, ball carrier
  renderer.ts           # Canvas 2D rendering
```

---

## Key Engineering Decisions

- **Team-agnostic pipeline** — All team-specific data flows from a single config file through a `getTeamConfig()` abstraction. No hardcoded team names anywhere in pipeline code.
- **Multi-provider LLM strategy** — Free tier (Gemini) handles 90% of LLM calls. Paid models (OpenRouter) only used for creative writing. Total cost: ~$0.004/article.
- **Separation of concerns** — Game engines (simulator, practice) are pure TypeScript with no React dependencies. UI components consume engine outputs. Everything is independently testable.
- **Type-driven development** — Shared types are single source of truth per subsystem. Types are updated first, code follows.

---

## Stack

`Next.js 16` · `React 19` · `TypeScript` · `Tailwind CSS 4` · `Zustand` · `MDX` · `Canvas 2D` · `Three.js` · `Rapier Physics` · `Vitest` · `Zod` · `Vercel`

---

*Source code is in a private repository. Visit [sportopias.com](https://sportopias.com) to see the live site.*
