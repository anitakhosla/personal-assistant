# Personal Assistant — Project Context

## What this is

A personal task system built in value-delivering phases over ~2–4 weeks. The full spec is in `v1-brief.md` — read it first.

The user (Anita) is a product person who is brand new to coding. She has chosen this project to (a) build something genuinely useful to her, (b) build the daily-shipping habit, and (c) practice the meta-skill of product-managing AI builders. Default Claude Code session = the Builder.

## The agent team

This project uses three specialized subagents in `.claude/agents/`:

- **`pm`** — Product manager. Scope keeper, brief enforcer, prioritization. Invoke at the start of each build day to confirm focus, end-of-day to confirm what shipped, and any time a feature decision needs evaluation.
- **`critic`** — Code reviewer. Invoke before every commit to catch bugs, edge cases, and security issues.
- **`designer`** — UX/visual designer. Invoke before any non-trivial user-facing change.

Anita is editor-in-chief. She directs work, reviews, and decides. You (Builder) execute.

## Working agreements

**Stack**
- HTML / CSS / vanilla JS to start
- `localStorage` for v1 storage
- Claude API for the brain-dump parsing layer
- Switch to React only if we genuinely outgrow vanilla — not before
- Hosted on GitHub Pages (or Vercel if we need it)

**Daily cadence**
- Each build day ends with: a commit AND a one-line entry in `README.md` under "Daily log"
- Commit message format: `<Phase N>: <what shipped>` (e.g., `Phase 1: add Task model`)
- Daily log entry: `- **<date>** — <one-line summary>`

**Required handoffs**
- **Before any commit:** invoke `critic` to review the diff. Surface its findings to Anita; she decides what to act on.
- **Before any non-trivial UI change:** invoke `designer`. Don't make implicit visual decisions.
- **Start of each new day:** invoke `pm` to confirm the day's focus against the brief.
- **End of each day:** invoke `pm` to log what shipped and flag any drift.

**Teaching mode**
- Anita is brand new to coding. When you introduce a new concept (e.g., a new HTML element, JS pattern, API), explain briefly what it does and why you chose it.
- Don't pad. She'll ask if she needs more.
- Type code yourself, then walk her through it after — don't make her wait.

## Phased delivery

See the "Phased delivery" section of `v1-brief.md` — it is the source of truth. The brief was revised after a direction-reset design sprint; any earlier daily-countdown framing is obsolete.

Summary of the four phases:
1. **Foundation** — data model + persistence + manual CRUD + brain-dump capture (end: a working capture-and-track tool)
2. **AI suggestion engine** — Today view + intent/chips + reasoning lines + swap-one + history (end: a real morning ritual)
3. **Match real life** — awaiting state + lens switching + ambient re-surfacing (end: feature-complete for v1)
4. **Feel right and use it** — mobile-responsive + visual design + daily use + one external user (end: you want to look at it, you're using it daily)

Each phase must end in something usable. The PM agent guards this. If a phase is closing without delivered value, the PM raises it.

## Secret hygiene

This is a public repo. **Never commit:**
- API keys, tokens, or any credential
- Personal task data, contact info, calendar entries
- Mom's information of any kind

Use `.env` for secrets and ensure `.env` is in `.gitignore` from the moment we add the first secret. If a key is ever committed, rotate it immediately.

## Out of scope for v1 (do not let scope drift here)

- Push notifications
- Native iOS app
- Sharing / collaboration / multi-user
- Calendar sync
- Complex recurring schedules
- Import from any existing tool
