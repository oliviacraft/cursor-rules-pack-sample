# Cursor Rules Pack v2 — Free Sample

**7 production-tested rules** from the full 50-rule pack.

These are not the obvious ones ("write clean code"). These are the rules that change how your AI coding assistant thinks about architecture, security, and tradeoffs.

→ **[Get all 50 rules for $27](https://oliviacraftlat.gumroad.com/l/wyaeil)**

---

## How to Use

1. Create `.cursor/rules/project.mdc` in your project root
2. Copy whichever rules apply to your stack
3. Replace `[brackets]` with your specifics
4. Cursor picks it up immediately — no restart needed

Works with **Cursor** and **Windsurf** (use `.windsurfrules`).

---

## The 7 Sample Rules

### Rule 1 — Dependency Discipline

```
Before suggesting a new npm package: (1) state what it does in one sentence, (2) check if it's actively maintained (last publish < 6 months), (3) confirm whether we could implement it in < 30 lines without the dependency. Prefer fewer, well-maintained packages. Never add a dependency for a task under 20 lines of code.
```

**Why this matters:** Every dependency is a future security vulnerability and maintenance burden. Left unchecked, AI coding tools will install a package for everything — including things a single utility function would handle.

---

### Rule 2 — Error Handling

```
Always wrap async operations in try/catch. Never swallow errors silently. Return typed error objects using a Result pattern or throw typed errors. Log errors with context: logger.error('[FunctionName] description', { error, context }). Always provide user-facing error states in UI components.
```

**Without this rule:**
```typescript
async function fetchUser(id: string) {
  const user = await db.user.findUnique({ where: { id } })
  return user // null if not found, undefined on error — caller doesn't know which
}
```

**With this rule:**
```typescript
async function fetchUser(id: string): Promise<User> {
  try {
    const user = await db.user.findUniqueOrThrow({ where: { id } })
    return user
  } catch (error) {
    if (error instanceof Prisma.NotFoundError) {
      throw new NotFoundError(`User ${id} not found`)
    }
    logger.error('[fetchUser] Unexpected error', { error, userId: id })
    throw new InternalError('Failed to fetch user')
  }
}
```

---

### Rule 3 — Comments Policy

```
Write self-documenting code first. Add comments only for: (1) non-obvious business logic — explain WHY, not WHAT, (2) workarounds — explain why the workaround exists and link to the issue, (3) complex algorithms — reference the algorithm name. Never comment what the code clearly does.
```

**Without this rule (useless comment):**
```typescript
// loop through users and send email if active
for (const user of users) {
  if (user.isActive) {
    await sendEmail(user)
  }
}
```

**With this rule (useful comment):**
```typescript
// Active-only: inactive users opted out per GDPR request #2847
// Re-evaluate this filter if subscription model changes
for (const user of users) {
  if (user.isActive) {
    await sendEmail(user)
  }
}
```

---

### Rule 4 — State Management Hierarchy

```
Follow this state hierarchy strictly:
- URL state → filters, pagination, search (useSearchParams)
- React state → UI-only, ephemeral (useState)
- Zustand → cross-component app state
- React Query → all server state

Never use Zustand to cache server data — that's React Query's job.
Never reach for Redux. If you're about to suggest Redux, stop and reconsider.
```

**Why this matters:** Unclear state ownership is the #1 source of stale data bugs. This rule forces a decision upfront, before the bug exists.

---

### Rule 5 — Parallel Data Fetching

```
Identify and parallelize independent data fetches. Never await sequentially when operations are independent — use Promise.all. When making a sequential await, add a comment explaining the dependency that forces the sequence.
```

**Without this rule (sequential waterfall):**
```typescript
const user = await getUser(userId)          // 80ms
const posts = await getPosts(userId)         // 60ms (waits for user)
const analytics = await getAnalytics(userId) // 90ms (waits for posts)
// Total: ~230ms
```

**With this rule (parallel):**
```typescript
const [user, posts, analytics] = await Promise.all([
  getUser(userId),
  getPosts(userId),
  getAnalytics(userId),
])
// Total: ~90ms (longest individual request)
```

---

### Rule 6 — Webhook Security

```
For incoming webhooks: verify the signature in the first 3 lines of the handler — reject immediately if invalid. Respond with HTTP 200 within 5 seconds — offload processing to a background job. Store the raw webhook event before processing. Implement idempotency using the event ID.
```

**Why this matters:** Most webhook implementations process the payload inline and skip signature verification. This leads to (1) spoofed events, (2) timeouts when Stripe/GitHub retries, and (3) duplicate processing when events are delivered twice.

**Stripe webhook pattern:**
```typescript
export async function POST(req: Request) {
  // 1. Verify signature immediately — before touching the body
  const body = await req.text()
  const signature = req.headers.get('stripe-signature')!

  let event: Stripe.Event
  try {
    event = stripe.webhooks.constructEvent(body, signature, env.STRIPE_WEBHOOK_SECRET)
  } catch {
    return new Response('Invalid signature', { status: 400 })
  }

  // 2. Store first — idempotency via upsert
  await db.webhookEvent.upsert({
    where: { stripeEventId: event.id },
    create: { stripeEventId: event.id, type: event.type, payload: event as any },
    update: {}, // already stored — no-op
  })

  // 3. Offload — respond 200 immediately, process async
  await inngest.send({ name: 'stripe/event.received', data: { eventId: event.id } })

  return new Response('OK', { status: 200 })
}
```

---

### Rule 7 — Database Query Safety

```
Never return full database records to the client — always use select to specify exactly which fields are needed. This prevents accidentally exposing password hashes, reset tokens, internal flags, and other sensitive fields.

For queries that could return more than 50 rows, always add pagination (take/skip or cursor-based).
```

**Without this rule:**
```typescript
// Returns password hash, resetToken, internalFlags, billingData — everything
const user = await db.user.findUnique({ where: { id } })
return NextResponse.json(user)
```

**With this rule:**
```typescript
const user = await db.user.findUnique({
  where: { id },
  select: {
    id: true,
    name: true,
    email: true,
    avatarUrl: true,
    subscriptionStatus: true,
    // password, resetToken, stripeCustomerId — never leave the DB unless explicitly needed
  }
})
return NextResponse.json({ data: user })
```

---

## What's in the Full Pack

The complete **Cursor Rules Pack v2** includes 50 rules across 5 sections:

| Section | Rules | Covers |
|---------|-------|--------|
| General Coding | 10 | TypeScript, error handling, naming, security, testing |
| Next.js & React | 10 | Server components, forms, state, auth, loading states |
| Database & Backend | 10 | Prisma, transactions, schema design, API patterns |
| AI Behavior | 10 | How the model approaches uncertainty, refactoring, reviews |
| Project-Specific | 10 | Templates for SaaS, APIs, CLI tools, and freelance client work |

→ **[$27 — instant download](https://oliviacraftlat.gumroad.com/l/wyaeil)**

Includes setup guide and a `.cursorrules` starter template you can drop into any project.

---

## Questions?

Open an issue or find me on X: [@OliviaCraftLat](https://x.com/OliviaCraftLat)
