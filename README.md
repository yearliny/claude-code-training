# Claude Code Training · 深入 Claude Code

A field-manual style presentation deck for getting development teams beyond surface-level use of [Claude Code](https://claude.com/claude-code).

Distilled from Anthropic's official [Best Practices](https://code.claude.com/docs/en/best-practices) and [Overview](https://code.claude.com/docs/en/overview) docs, with a worked case study on a real production codebase.

## Contents

13 chapters, single-page scroll:

1. **Prologue** — the one constraint that explains everything else
2. **The Map** — four concentric layers (Tools / Memory / Extensions / Orchestration)
3. **The Three Layers** — Skills × Subagents × Hooks decision matrix
4. **Workflow** — Explore → Plan → Code → Commit
5. **Verification** — the single highest-leverage practice
6. **CLAUDE.md Discipline** — what to include, what to cut
7. **Context Management** — `/clear`, `/rewind`, subagent offloading
8. **Prompt Precision** — before/after pairs
9. **Failure Patterns** — the five traps
10. **Scaling Out** — headless, worktrees, fan-out, Writer/Reviewer
11. **Case Study** — a real repo's `.claude/` asset tree
12. **The Workshop** — a half-day agenda you can run on Monday
13. **Coda** — develop your own intuition

## Run locally

It's one HTML file with CDN fonts. Just open it.

```bash
# any static server works
npx serve .
# or
python -m http.server 8000
```

Or open `index.html` directly in a browser.

## Deploy

Deployed via [Cloudflare Pages](https://pages.cloudflare.com/). Any static host works — there's no build step.

## Keyboard

- `↑` / `↓` / `Space` / `PageUp` / `PageDown` — jump between chapters
- `Home` / `End` — first / last chapter

## Credits

- Content distilled from Anthropic's [official Claude Code docs](https://code.claude.com/docs/en/overview)
- Typography: Instrument Serif · Newsreader · JetBrains Mono · Noto Serif SC

## License

MIT — see [LICENSE](LICENSE).
