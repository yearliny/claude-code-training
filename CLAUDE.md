# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A single-file, static HTML presentation deck — a "field manual" about Claude Code itself, delivered to an internal hospital engineering team (智慧医院团队). Content is bilingual (Chinese body, English headlines/jargon), distilled from Anthropic's official Best Practices and Overview docs.

**There is no build step, no package manager, no framework.** Everything lives in `index.html` (~2000 lines): inline `<style>`, inline `<script>`, and 15 `<section class="spread">` elements (cover + 14 chapters). Fonts load from Google Fonts CDN at runtime.

## Run / preview

```bash
npx serve .              # any static server
python -m http.server 8000
# or just open index.html in a browser
```

Deployed to Cloudflare Pages — no build, just upload.

## Architecture conventions

- **Each chapter is one `<section class="spread" id="...">`.** The 15 IDs (`cover`, `prologue`, `map`, `layers`, `workflow`, `verify`, `claudemd`, `context`, `prompt`, `failures`, `scaling`, `repo`, `governance`, `workshop`, `coda`) are referenced in three places that must stay in sync: the section itself, the margin `<nav class="index">` links (`#cover` … `#coda`), and the keyboard navigation script at the bottom which queries `section.spread` and `.index a` in document order. Adding or reordering a chapter requires updating all three, plus the folio counters (`XX / 14`) and the cover-side chapter count.
- **All CSS lives in one `<style>` block in `<head>`**, organized by labeled banner comments (`/* ============================ MASTHEAD ============================ */`, etc.). Follow the same banner style when adding new components. Design tokens (surface, border, text, accent) are CSS custom properties on `:root` — reuse them rather than hardcoding values. Legacy aliases (`--ink`, `--paper`, `--rule`, `--blue`) are kept for compatibility but new code should use the modern names (`--text`, `--bg`, `--border-strong`, `--ok`).
- **Three typefaces, each with a job:** `--font-display` (Inter Tight, sans-serif headlines), `--font-body` (Inter, prose), `--font-mono` (JetBrains Mono, eyebrows/folios/metadata/code). Chinese fallback is Noto Sans SC. Don't introduce a fourth.
- **Visual language is "modern dev tool" / light tech, projection-oriented**: near-white background (`--bg: #fafbfc`) with very faint cyan radial glow, deep cyan accent (`--accent: #0891b2` — deep enough to survive projector washout), Inter sans-serif, monospace eyebrows in caps, thin 1px borders, subtle elevation via white `--bg-elevated`. **Exception**: code blocks (`pre`, `.repo-tree`) keep a dark background (`--bg-code: #0d1117`) — high-contrast dark-on-white is the Vercel/Stripe-docs convention and looks more "tech" than monochrome code. NO paper grain, NO italic-serif emphasis, NO print-style drop shadows, NO round ink stamps. Emphasis is done via accent color + weight 500, not italic.
- **Sizing is tuned for projection** (audience viewing from across a room): base body font-size is 18px (not the usual 16); pre code is 14px; card paragraphs are 15-16px; table cells 16px; subheadings start at 24px. Don't shrink these "for density" — readability from 5-10m beats information density on a projector. Larger headlines (e.g., chapter h2 `clamp(40px, 5.4vw, 80px)`) and the cover title (`clamp(64px, 12vw, 200px)`) are intentionally cinematic.
- **Responsive breakpoint at `max-width: 900px`** collapses the margin index and adjusts grid layouts. Test any new layout there.

## Content notes

- Audience is an internal hospital IT team with weak English. **Default to Chinese for all conceptual language**; keep English only for filenames, CLI commands, protocol/standard acronyms (MCP, LSP), proper nouns, and Claude Code's officially-fixed terms (harness, agentic — annotate on first use). Translate session→会话, context→上下文, commit→提交, diff→改动, review→评审, ship→上线, compact→压缩, ticket→任务. Avoid mid-sentence English/Chinese ping-ponging — it breaks reading flow for this audience.
- **Teaching framework — every technique must be written as point → why → example**:
  1. **抓重点** — open with the core claim in one or two sentences.
  2. **解释为什么** — explain the mechanism / cost / first-principles reason, *ideally backed by a number* (token counts, percentages, real-world time, frequency). Asserting "X is the most important practice" without explaining why = audience cannot internalize. This was the dominant failure mode of the pre-2026-05-21 draft.
  3. **举例子** — a concrete scenario, before/after, or numbers applied to a real task (preferably from the `JeecgBoot/hospital` repo) so the reader can *see* it.
  Apply this to chapter prose, card descriptions, and margin-notes — anywhere a technique or rule is being taught. It does NOT apply to navigation, schedules, or reference tables.
- The case study references `JeecgBoot / hospital` and `.claude/` asset trees from that real repo. Treat repo-specific references in the `repo` chapter as factual examples, not placeholders.
- External links to `code.claude.com/docs/...` and `claude.com/blog/...` are authoritative source citations — don't replace or remove them when editing content.
