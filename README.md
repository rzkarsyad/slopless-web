# slopless-web

A Claude skill for designing websites that don't look AI-generated.

Instead of starting from "a modern landing page", Claude starts from **real references**: sections pulled from [Mobbin](https://mobbin.com) and live websites captured section by section. It tears them down, writes a design direction, builds the page, and then audits the result against a list of common AI-slop patterns.

```
Brief → References (Mobbin + URLs) → Teardown → Design Direction → Build → Slop audit → Fix
```

## What it does

- **Mobbin references**: one search per section (hero, pricing, footer…), 2–3 picks per section with a reason for each
- **Live URL capture**: screenshots each section of a site and extracts real tokens (fonts, sizes, colors, spacing) with `getComputedStyle`
- **HTML to design**: optionally rebuilds captured sections as clean, tokenized HTML or Figma frames for study
- **Design Direction**: a required `direction.md` (concept, tokens, signature moves, reference for each section) before any building
- **Slop audit**: checks visuals and copy against a blacklist (purple gradients, the hero + 3 cards template, fake metrics, "elevate/seamless/unlock"…) and fixes the hits

## Install

### As a plugin (recommended)

This repo is a plugin marketplace. In Claude Code:

```
/plugin marketplace add rzkarsyad/slopless-web
/plugin install slopless-web@slopless-web
```

Pick up future updates with `/plugin marketplace update slopless-web`.

In the Claude desktop app, add `rzkarsyad/slopless-web` (or `https://github.com/rzkarsyad/slopless-web`) as a plugin marketplace from the plugins screen, then install **slopless-web**.

### Manual copy

```bash
git clone https://github.com/rzkarsyad/slopless-web
mkdir -p ~/.claude/skills
cp -r slopless-web/skills/slopless-web ~/.claude/skills/
```

### Claude app skill upload

Zip the `skills/slopless-web` folder and upload it in Claude's Skills settings.

## Recommended connections

| Tool | Why | Required? |
|---|---|---|
| Mobbin MCP | Reference search for sections, screens, flows | Recommended |
| A browser MCP (Playwright, Chrome, etc.) | Per-section screenshots and token extraction from live URLs | Recommended |
| Figma MCP | When the output should be Figma frames | Optional |

Without Mobbin or a browser, the skill still works from URLs and the brief, just with fewer references.

## Usage

```
Use slopless-web to design a landing page for <product>.
Audience: <who>. Main action: <book a call / sign up / buy>.
Tone: <3 concrete words>. Output: HTML / Figma / Next.js.
References I like: <urls>
```

## Example

`examples/magercoding/direction.md` is a real Design Direction produced by the skill for a studio landing page: concept, tokens, and how each section maps to its Mobbin reference.

## Notes

- References are for learning structure and decisions. The skill never ships another brand's logo, imagery, copy, or a pixel clone.
- Mobbin image links expire; download anything you want to keep.

## License

MIT
