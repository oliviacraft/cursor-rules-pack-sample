# Cursor Rules Pack — Free Starter Kit

> Pre-built `.mdc` rules and `CLAUDE.md` templates for developers using Cursor Agent Mode and Claude Code.

**Free starter** → [oliviacraftlat.gumroad.com/l/pomoo](https://oliviacraftlat.gumroad.com/l/pomoo)
**Full pack (50 files, 14 stacks)** → [oliviacraftlat.gumroad.com/l/wyaeil](https://oliviacraftlat.gumroad.com/l/wyaeil) — $27

---

## The problem this solves

Every new Cursor or Claude Code session starts blank. The model doesn't remember your conventions, architecture decisions, or "never do X" rules.

You re-explain them every session. Or you write a rules file once, accumulate 400 lines, and watch it fail silently after context compaction.

This kit gives you a structured, minimal starting point that actually works.

---

## What's included (free starter)

- `CLAUDE.md` template — three-section structure that survives compaction
- `.cursor/rules/` templates for TypeScript, Python, Go, React
- Anti scope creep rule
- Compaction amnesia prevention checklist
- Context bloat prevention rules

---

## Gists (copy-paste ready)

| Gist | Use case |
|------|----------|
| [How to set up .mdc for multi-language repos](https://gist.github.com/oliviacraft/281f8ba971d238e8ff0ae87e2e99f21c) | Python + Java + TypeScript in one project |
| [Anti scope creep .mdc rule](https://gist.github.com/oliviacraft/2b2fbfcb0c3541ee1768be9a2a379eba) | Prevent agent from expanding task scope |

---

## Articles

| Article | Pain addressed |
|---------|---------------|
| [How to Fix Cursor Compaction Amnesia](https://dev.to/olivia_craft/how-to-fix-cursor-compaction-amnesia-and-why-your-rules-stop-working-1c19) | Rules stop working after context compaction |

---

## Common failures this fixes

**Rules ignored in Agent Mode** → scope your `.mdc` with proper globs, not a single root `.cursorrules`

**Context lost after compaction** → three-section CLAUDE.md, hard constraints first

**Scope creep across sessions** → explicit scope constraints in always-apply rule

**Rules deleted on Cursor launch** → migrate from root `.cursorrules` to `.cursor/rules/*.mdc`

---

## Full pack

50 `.mdc` files across 14 stacks: React, Next.js, TypeScript, Go, Python, FastAPI, Rails, Spring Boot, Laravel, Flutter, Swift, Android, Kotlin, Rust.

Each file: properly scoped globs, activation mode set, tested in Agent Mode.

→ [oliviacraftlat.gumroad.com/l/wyaeil](https://oliviacraftlat.gumroad.com/l/wyaeil) — $27 one-time

---

Built by [@OliviaCraftLat](https://x.com/OliviaCraftLat)
