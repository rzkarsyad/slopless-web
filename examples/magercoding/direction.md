# Magercoding — Design Direction

## Brief
- Studio: product design + frontend/full-stack, based in Purwokerto, Central Java (UTC+7)
- Audience: startup founders/PMs in US, UK, AU
- One action: **Book a 30-min call**
- Tone: editorial, calm, confident. Copy in English.

## Concept (one sentence)
**"The studio ledger"** — the page reads like a well-kept project ledger from a small studio on the other side of the world: ruled lines, monospace margin notes, a real index of shipped work, and time zones treated as a feature ("you brief us at 6pm, you wake up to progress").

## Teardown → what we borrow (principle, not pixels)

| Ref | Borrow | Skip |
|---|---|---|
| [Cloudstudio hero](https://mobbin.com/sites/sections/bd08f963-ed5b-425f-b282-a6040e95fff1) | Meta row under the CTA: labelled facts (new projects / based in / how it starts) | Loud sans display, pastel bg |
| [Frontify hero](https://mobbin.com/sites/sections/9dc7cb3d-08cc-4c17-bb89-4373060676f2) | Huge serif headline left, tiny supporting text + CTA pushed right | — |
| [Locomotive work index](https://mobbin.com/sites/sections/280c1a2d-41d4-4495-a4bd-816763c93ad3) | Work as a typographic index (name / category / market), no thumbnails needed | — |
| [Vucko services](https://mobbin.com/sites/sections/72f31890-b4dd-46f4-b6f6-11ce33361d24) + [Koto](https://mobbin.com/sites/sections/968754c4-c525-4315-a823-07721be58b1b) | Giant numeral + (label) + statement, ruled sub-list | Image cards |
| [Wild process](https://mobbin.com/sites/sections/1bac0acb-c4fe-46ec-acd7-fe0bf057faf2) | Mono "PHASE 1 · WKS 1–2" labels on a ruled timeline | 4 colored squares |
| [Mother Design footer](https://mobbin.com/sites/sections/23a43fc2-e616-4b49-945c-4a0dd97df268) | Full-bleed wordmark + city with live local time | Newsletter form |
| [YLLW CTA row](https://mobbin.com/sites/sections/71ec7c29-2e27-4702-ac7b-b26ccea5d8a0) | Full-width ruled CTA line with arrow | Condensed caps |

## Tokens
- **Display**: Newsreader (Regular + Italic), optical, tight tracking (-2%)
- **Text**: IBM Plex Sans 400/500
- **Meta**: IBM Plex Mono 400, 11–12px, uppercase, +6% tracking
- **Type scale** (1440): 12 / 15 / 18 / 24 / 40 / 64 / 120 / 200
- **Color**
  - `paper` #F2EFE8 — background
  - `ink` #1A1A17 — text, rules on dark
  - `muted` #6B675E — secondary text
  - `rule` #D3CDBF — hairlines
  - `clay` #B5461E — accent (terracotta roof tile of Central Java). Max 3 uses on the page: CTA, live dot, one italic word.
- **Spacing**: 4 / 8 / 16 / 24 / 40 / 64 / 120 / 200
- **Radius**: 0 everywhere, CTA pill 999 is the only exception
- **Shadows**: none. Structure comes from 1px rules.
- **Container**: 1440 frame, 40px side margins, 12-col grid, 24 gutter

## Layout system
Every section starts with the same margin note row (mono label left, running index right: `02 / 06`). Content then breaks the grid differently per section: hero left-heavy, services numeral-left, work full-width table, process horizontal, footer full-bleed wordmark. No two consecutive sections share an alignment.

## Signature moves
1. **Two clocks**: header shows "Purwokerto 07:40 · Your time 19:40 (SF)". Repeated in the process section as the overnight handoff.
2. **Work as an index**, not a card grid.

## Sections
1. **Nav + Hero** — Frontify + Cloudstudio
2. **Work index** — Locomotive
3. **Services** (3: Product design · Design systems · Frontend build) — Vucko/Koto
4. **Process** (Call → Proposal → Sprints → Handoff) — Wild
5. **Overnight** (time zone argument) — original, from the concept
6. **CTA row + Footer** — YLLW + Mother Design

## Motion (for build later)
Rules draw in left→right 400ms ease-out on enter. Clock ticks. Nothing else.

## Copy voice
- Say the specific thing: weeks, deliverables, time zones. No adjectives doing the work.
- Short declaratives. One italic word per headline max.
- Never "elevate / seamless / unlock / cutting-edge".

Example headlines:
- "Product design and frontend, *shipped* while you sleep."
- "Brief us at 6pm. Review at 9am."
