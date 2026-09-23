---
name: slopless-web
description: Build distinctive, non-generic websites from real references - Mobbin sections/screens and live URLs captured per section, analyzed into a design direction, then built as HTML, React or Figma. Use when asked to design or build a landing page or website that should not look AI-generated.
---

# Slopless Web

Reference-driven website design. Every design decision traces back to a real reference or to the brief, never to "what an AI landing page usually looks like".

Pipeline: **Brief → Collect references (Mobbin + URLs) → Teardown → Design Direction → Build → Slop audit → Fix**.

Do the phases in order. Do not start building before the Design Direction exists.

## Requirements

- **Mobbin MCP** (recommended): tools `search_sections`, `search_screens`, `search_flows`. Without it, rely on URLs the user gives.
- **A browser tool** for live URL capture (any MCP browser: Playwright, Chrome extension, built-in browser). Without it, fall back to fetching page text only.
- **Figma MCP** (optional) if the output target is Figma.

---

## Phase 0 - Brief

Get (ask in one batch only what's missing; otherwise proceed):
- Product, audience, the ONE thing the site must make people do
- Brand assets if any (logo, colors, fonts, existing site)
- Tone in 3 concrete words (not "modern, clean" - e.g. "editorial, dry, confident")
- Reference URLs the user likes (optional)
- Output target: HTML page (default), Figma frames, or production code (React/Next)
- Real copy, or permission to write copy from the brief

Write a section list for the page (e.g. hero, proof, how-it-works, pricing, FAQ, footer). Each section = one reference hunt.

---

## Phase 1a - Mobbin references

Tools: `search_sections` (web sections), `search_screens` (platform `web` or `ios`), `search_flows` (multi-step journeys).

Rules:
- One section per query. Describe content + elements, not style words. Good: "pricing section with three plans and annual toggle". Bad: "modern clean pricing".
- Use the SAME `task_intent` string (English) for every call in this task.
- `limit` 8-12 per query to keep context sane. Paginate only if nothing fits.
- Name a specific app/company in the query when the user wants that brand's approach.
- LOOK at the returned images. Never judge a reference by its metadata.
- Per section, shortlist 2-3 references. Record: `mobbin_url`, `image_url`, and one line on WHY it's picked.
- If images must be kept (Figma, docs, moodboard), download from `image_url` (links expire). Cite with `mobbin_url`.
- Actively reject references that are themselves generic (see slop list below). Mobbin has plenty of those too.

---

## Phase 1b - Live URL capture (per-section snapshots)

Use a browser tool. If none is available, fetch the URL for structure and copy only, and tell the user screenshots weren't possible.

Capture procedure:
1. Open the URL at desktop width (~1440px). Dismiss cookie banners.
2. Identify section boundaries (`<section>`, `<header>`, `<footer>`, large landmark blocks). If a JS/eval tool exists, list them with their top offset and height.
3. Scroll section by section and screenshot each one. Name them `ref-<site>-<nn>-<section>.png`.
4. Also capture at mobile width (~390px) for hero + one dense section.
5. Extract real tokens via JS when possible: `getComputedStyle` on body, h1-h3, p, buttons, links, cards → font-family, font-size, line-height, letter-spacing, weights, colors, background, border-radius, section padding, container max-width. Write them to `ref-<site>-tokens.json`.
6. Note motion: what animates on scroll/hover, durations, easing.

Token extraction snippet:

```js
const pick = s => { const el = document.querySelector(s); if (!el) return null;
  const c = getComputedStyle(el);
  return { font: c.fontFamily, size: c.fontSize, lh: c.lineHeight, ls: c.letterSpacing,
           weight: c.fontWeight, color: c.color, bg: c.backgroundColor, radius: c.borderRadius }; };
JSON.stringify(Object.fromEntries(['body','h1','h2','h3','p','a','button'].map(s => [s, pick(s)])), null, 2);
```

"HTML to design" option: for each captured section, rebuild it as clean, tokenized static HTML (`ref-<site>-rebuild.html`) - semantic structure, CSS variables, no original scripts. This is a study copy for analysis. If the user wants it in Figma, push it via the Figma MCP: one frame per section, auto-layout, tokens as variables.

Legal/ethical line: references are for learning structure, rhythm and decisions. Never ship another brand's logo, illustrations, photos, copy, or a pixel clone as the final output.

---

## Phase 2 - Teardown

For each shortlisted reference, write a short teardown (bullets, not prose):
- **Grid & layout**: columns, asymmetry, alignment, what breaks the grid
- **Type**: families, scale ratio, weight contrast, case, tracking, measure
- **Color**: base, ink, accent(s), how much accent is used (usually very little)
- **Density & rhythm**: section padding, gaps, how whitespace is distributed
- **Signature move**: the one decision that makes it memorable
- **Steal / skip**: what to borrow as a principle, what is generic and should be ignored

---

## Phase 3 - Design Direction (required before building)

One short document (`direction.md`), shown to the user before building if they are present:
- **Concept in one sentence** tied to the product (e.g. "a lab notebook: ruled grid, marginalia, monospace annotations")
- **Tokens**: type pairing (display + text, real font names), type scale, color palette (hex, with roles), spacing scale, radius, border/shadow policy, container width
- **Layout system**: grid, how sections vary so the page isn't a stack of identical blocks
- **Signature move(s)**: 1-2, max
- **Per section**: which reference(s) it draws from + the principle borrowed
- **Motion**: few, purposeful, with durations
- **Copy voice**: 3 rules + 2 example headlines written from the brief

See `examples/magercoding/direction.md` in this repo for a filled-in example.

---

## Phase 4 - Build

Default output: one self-contained HTML file (inline CSS/JS, fonts via Google Fonts).

- All tokens as CSS custom properties on `:root`. No magic numbers scattered in rules.
- Build section by section in the order of `direction.md`; each section's HTML comment names its reference.
- Semantic HTML, real alt text, visible focus states, `prefers-reduced-motion` respected, contrast AA.
- Responsive from 360px to 1600px, no horizontal scroll.
- Images: use real brand assets if given; otherwise typographic/graphic solutions or clearly labeled placeholders. Never fake product screenshots, logos, or testimonials.
- Figma output: variables for tokens, one frame per section, auto-layout everywhere.
- React/Next output: same tokens as a theme file, one component per section.

---

## Phase 5 - Slop audit (mandatory)

Screenshot the built page at desktop and mobile. Check against this list. Every hit must be fixed or explicitly justified by the brief.

**Visual slop**
- Purple/indigo/blue-violet gradient anything; gradient text headlines
- Inter/Roboto/system font for everything with no display face
- Centered hero → 3 equal feature cards with icons in rounded squares → testimonial grid → CTA band (the default template)
- Emoji or generic icon-set icons as the main visual language
- Every card same size, same large radius, same soft shadow
- Glassmorphism, floating blurred blobs, random glows, grain added for no reason
- Fake dashboard mockups, fake logo bar, fake metrics ("10x faster", "99.9%")
- Every section identical padding and centered alignment
- Dark mode + neon accent by default with no brand reason
- The "tasteful AI" default: cream background + serif + mono labels with nothing specific to the product. Allowed only when a signature move ties it to the brief.

**Copy slop**
- "Unlock", "Elevate", "Supercharge", "Seamless", "Revolutionize", "Empower", "Next-level", "Game-changer"
- "X, reimagined" / "The future of X" / "Built for the modern Y"
- Triplets everywhere (fast, simple, powerful)
- Headlines that could fit any product. Test: swap in a competitor's name - if it still works, rewrite.

**Pass criteria**
- A stranger could describe the concept from the screenshot alone
- At least one layout decision that isn't centered/symmetric
- Type does real work (scale contrast, a display face, deliberate measure)
- Accent color is used sparingly and meaningfully
- Every section can point to its reference or brief reason

Report the audit as a short table: item → pass / fixed / justified. Then deliver.

---

## Delivery

- The built page (or Figma file), `direction.md`, and a references list (section → `mobbin_url` / source URL).
- Optional: the moodboard (downloaded reference images) and captured section screenshots if the user wants to keep them.
- One line on what to try next (e.g. an alternate direction), not a recap of steps.
