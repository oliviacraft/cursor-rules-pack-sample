# Cursor Rules Pack — Sample Plugin

A **[Open Plugins](https://open-plugins.com)**-compatible plugin with 7 production-tested Cursor Rules for TypeScript projects.

→ **[Get the full 50-rule pack for $27](https://oliviacraftlat.gumroad.com/l/wyaeil)**

---

## Structure

```
cursor-rules-pack-sample/
├── .plugin/
│   └── plugin.json     # Open Plugins manifest
├── rules/
│   ├── core.mdc        # Always-active: dependency discipline, error handling, naming
│   ├── nextjs.mdc      # Next.js App Router rules
│   ├── database.mdc    # Prisma, API security, webhook idempotency
│   └── patterns.mdc    # Data fetching patterns
└── .cursorrules        # Legacy Cursor format (same rules)
```

---

## Rules Included

### `rules/core.mdc` — always active
- **Dependency Discipline** — evaluate packages before installing; never add one for < 20 lines
- **Explicit Error Handling** — typed errors, no silent failures, log with context
- **Comments Policy** — explain WHY not WHAT; workarounds get an issue link
- **Naming Conventions** — PascalCase, camelCase, booleans start with `is`/`has`/`can`
- **File Size Discipline** — under 200 lines, co-locate related files

### `rules/nextjs.mdc` — Next.js App Router projects
- Server Components First — default to RSC, explain every "use client"
- State Management Hierarchy — URL → React → Zustand → React Query
- Parallel Data Fetching — Promise.all over sequential awaits
- Loading & Error States — skeleton components, actionable error messages

### `rules/database.mdc` — backend/API files
- Database Query Safety — always use `select`, paginate > 50 rows
- API Route Security — auth → validate (Zod) → authorize → respond
- **Webhook Security** — verify signature first, respond in 5s, idempotency via upsert
- Prisma Best Practices — transactions, indexes, schema standards

### `rules/patterns.mdc` — optional patterns
- Before/after code examples for parallel fetching and typed error results

---

## Installation

**Via Open Plugins-compatible tool (e.g. cursor.directory):**
Install directly — rules are auto-discovered from `rules/*.mdc`.

**Manual:**
Copy individual `.mdc` files to your `.cursor/rules/` directory.

**Legacy `.cursorrules`:**
Copy the `.cursorrules` file to your project root.

---

## What's in the Full Pack

| Section | Rules | Covers |
|---------|-------|--------|
| General Coding | 10 | TypeScript, error handling, naming, security, testing |
| Next.js & React | 10 | Server components, forms, state, auth, loading states |
| Database & Backend | 10 | Prisma, transactions, schema design, API patterns |
| AI Behavior | 10 | Uncertainty handling, refactoring, code review |
| Project Templates | 10 | SaaS, APIs, CLI tools, freelance client work |

→ **[$27 — instant download](https://oliviacraftlat.gumroad.com/l/wyaeil)** | Includes setup guide and per-project-type starter templates.

---

[@OliviaCraftLat](https://x.com/OliviaCraftLat) · [oliviacraft.lat](https://oliviacraft.lat) · MIT License
