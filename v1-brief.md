# Project Brief — v1 (revised)

_Brand-new coder · ~2 hours/day · phased delivery over 2–4 weeks_
_Working name: TBD_
_Last revised after a direction-reset design sprint_

---

## Changed in this revision

The previous brief positioned the home view as a category dashboard. After a sprint, that was wrong. This revision flips the architecture:

- **Home view is now "Today"** with AI-suggested picks (was: category dashboard)
- **Data model simplified to two levels:** Goals → Tasks (was: Goals → Tasks → Subtasks)
- **AI suggestion engine is now the centerpiece feature** of v1
- **Categories demoted to ambient context** (was: primary navigation)
- **Build plan structured as value-delivering phases** (was: daily countdown)

Previous-direction artifacts that don't serve the new architecture should be archived or deleted, not preserved.

---

## What / why

**What:** A self-organization system that surfaces daily tasks based on how I want to prioritize my life.

**Why:** There are many tools out there for task management. But none of them really fit my needs. Most task management systems are just checklists, with no intelligent layer behind them.

What I need is not just a task list, but a "personal assistant" that helps me stay on top of all the things I need to get done. This assistant should:

- Break things down so I can make small progress against my list of to-dos and not get overwhelmed
- Help me see my progress over time, since it's easy to lose sight of progress in the face of a never-ending list
- Help me balance my priorities based on what is important to me in life — if a certain area of life is not getting attention, it should gently nudge me toward that

For the MVP, it takes inputs from a list I manually curate. **Post-v1**, it should integrate with my calendar and email — and potentially other sources — to pull data and understand where my energy and focus are actually going, so it can help rebalance.

The intelligence layer is what separates this product from any other task management tool, because it understands me and my priorities. Over time, as it learns more about me, manual entry should shrink.

### What the intelligence layer must balance

- Urgent vs. important
- Short-term vs. long-term
- Multi-step goals
- Tactical tasks vs. goals / aspirations
- Areas of life (work, health, finances, family, etc.) — so all are being addressed
- Intelligent follow-up of tasks, when required
- Separation of task lists (my to-do vs. what I need to do for Mom)

### Why this and not another todo app (sharper version)

Generic todo apps fail in four places: granularity (aspirations sit next to one-off calls), timeframe (no good "when"), follow-up (things drop after the first action), and — least-named — **picking** (they hand you the full list every day and let you fend for yourself). This system treats picking as the central job, not an afterthought.

---

## JTBD

> When I start my day, and during check-ins throughout, I want to see today's concrete actions — sized as baby steps I can actually complete — so I never get stuck in "what am I doing right now?" and the things that matter to me actually move forward.

This is the spec. Every design decision below ladders up to it.

---

## The user

Anita. Mom is the second lens, also P0 (not stretch).

---

## The opinionated bets

1. **Today is the home — and the AI proposes it.** The default view isn't a category dashboard, a goal list, or a backlog. It's today: 3-5 baby steps proposed each morning with reasoning, accepted / swapped / removed by the user. This is the core mechanic.

2. **Two levels only: goals and tasks.** Goals (optional, multi-step) contain tasks. Tasks can be standalone. If a third level seems necessary, split into more tasks at level two.

3. **Brain-dump in, structure out.** Capture happens in the user's own words. The system asks one clarifying question if needed and shapes it into the right object.

4. **"Awaiting" is a first-class state.** Many tasks aren't done when you mark them done — they're waiting on someone or something. The system tracks who, when to nudge, and what's next.

5. **No-deadline tasks don't disappear.** Ambient tasks re-surface through the AI suggestion engine periodically. They don't nag, they don't get buried forever.

6. **Multiple lives are first-class.** A lens switcher between You and Mom. Same app, separate data, separate everything.

7. **Categories for awareness, not navigation.** Visible on each row and in a balance strip at the bottom of Today. Not the structure of the app.

---

## Data model

- **Goal** (optional)
  - Belongs to a Lens (You / Mom)
  - Has a Category (Career / Finances / Health / Hobbies / Family / Personal Growth / Home)
  - Contains many Tasks
  - Never "done" — just retired when no longer relevant

- **Task**
  - Belongs to a Lens
  - Has a Category (inherited from parent Goal, or set directly when standalone)
  - May belong to a Goal, or stand alone
  - Has a status: active / awaiting / done
  - If awaiting: tracks who/what we're waiting on + nudge date
  - May have a deadline, or be "ambient" (no deadline)
  - Has a freeform notes field for informal sub-steps

Two object types. No subtasks. If a task feels too big, split into multiple tasks at the same level.

---

## The home view: "Today"

The default screen. Rough layout:

```
TODAY · [date]
─────────────────────────────────

📝 Anything I should know?    [energy chip] [time chip]


Suggested for today:

  ⃝  [Task]
      [Goal · ]Category
      → [Reasoning, ≤8 words]

  ⃝  [Task]
      ...

   [✓ Looks good]   [↻ Show alternatives]

─────────────────────────────────

Goals that haven't moved:
  · [Goal name] · 23 days

Last 14 days · category balance:
  ▓▓▓▓▓░░░░░░░░░  Career / Finances / Health / Hobbies / Family / Personal Growth / Home
```

Top: proposed list with reasoning. Middle: lock-in / swap-one. Bottom: ambient signals (stalled goals, category balance). A single tab "Plan" leads to the goal hierarchy and full task pile for deliberate review.

Two modes, one screen:
- *In-day:* mark done, capture new (system asks "today, or save for later?", defaults to "later")
- *Morning planning:* tap "Plan" → see goals and full task list → return to Today

---

## The AI suggestion engine (centerpiece)

### Inputs

1. **Implicit (learned from history)**
   - Suggested-vs-completed patterns
   - Time-of-day completion patterns
   - Goal engagement frequency
   - Modification patterns (kept / swapped / removed)

2. **Explicit (user tells it)**
   - Daily intent (single sentence, optional)
   - Energy + time chips (default: medium / 1hr)
   - Optional "boost this goal" toggle (stretch)

3. **Structural (task aging)**
   - Days since task creation
   - Days since parent goal touched
   - Deadlines approaching
   - Ambient re-surface windows
   - Awaiting tasks ready for nudge

### Mechanism

Each morning, an LLM call is fed recent history + current goal state + today's intent + chips. It returns 3-5 tasks, each with a one-sentence reasoning line (≤8 words). "Show alternatives" swaps one item with another candidate (keeps what was liked). The system stores every suggestion + modification + completion for future calls. No ML training — just an LLM with good context.

### Design choices already locked

- 3-5 items per day, upper bound shrinks when energy is low
- Reasoning line ≤8 words, one per row
- "Show alternatives" swaps one item, not the whole list
- Pre-populated when app opens, refreshable
- Energy/time per-day, defaults to medium / 1hr

---

## In scope for v1 — must-have core

- **Today view** with AI-suggested picks and reasoning lines
- **AI suggestion engine** (the centerpiece)
- **Goals + tasks data model** (two levels, localStorage persistence)
- **Brain-dump capture** with AI parsing into goals/tasks
- **Categories on each row + balance strip at bottom**
- **"Awaiting" state** with nudge logic + "what's next" prompt
- **Multi-life lens switching** (You / Mom)
- **Responsive web app** (phone browser + desktop)
- **Ambient task re-surfacing** integrated into suggestion engine

## Stretch (cut first if time runs short)

- Job-search starter pack (pre-loaded goal + tasks)
- "Considering" parking lot for maybe-tasks, weekly review
- "Boost this goal" toggle
- "Explain more" deep-reasoning tap on each row
- Auto-suggest next step from same goal on completion
- Category balance flagging (proactive: "Health has gone dark for 2 weeks")

## Out of scope for v1

- Push notifications, native iOS app
- Sharing, collaboration, multi-user accounts (beyond You/Mom lens)
- Complex recurring schedules
- Import from existing tools
- Public release as a product

## Beyond v1 — the broader vision

These are not v1 features and not stretch — they are deliberate future directions that the product is meant to grow into. Naming them keeps the v1 architecture honest (it should not foreclose them) without bloating scope.

- **Calendar + email integration.** Pull data from calendar and email (and potentially other sources) so the system can see where my energy and focus are actually going, and rebalance suggestions accordingly. The MVP relies on a manually curated list; over time, manual entry should shrink.
- **Goal progress view.** A dedicated surface to see progress against goals over time — because it's easy to lose sight of progress in the face of a never-ending list. v1 hints at this via "goals that haven't moved" and the 14-day category balance strip, but a real progress view is post-v1.

---

## Stack

- Single-page web app — HTML / CSS / vanilla JS to start; React only if vanilla genuinely cracks
- `localStorage` for v1 persistence
- Claude API for parsing + suggestion engine
- Hosted on GitHub Pages or Vercel (free)
- VS Code + Claude Code with the agent team (pm / critic / designer)

---

## Phased delivery

The build is structured as four phases, each ending in something usable. Roughly a week each at ~2 hours/day, fitting inside a 2–4 week window depending on real-life pace. The point is not to hit a day count — it's that each phase delivers something of value, so if life intervenes between phases I still have something working.

### Phase 1 — Foundation: capture and track

Data model (Goals, Tasks) with localStorage persistence. Manual CRUD via a simple form. Brain-dump capture box wired to the Claude API for parsing into the data model.

**Value at end of phase:** I can dump my thoughts into the app and have them structured into goals/tasks, then edit and check them off. A working personal capture-and-track tool, even before the intelligence layer.

### Phase 2 — The centerpiece: AI suggestion engine

Today view as the home screen. Daily intent + energy/time chips. AI proposes 3–5 tasks each morning with reasoning lines. "Show alternatives" swaps one item. History tracking so the engine learns over time.

**Value at end of phase:** A real morning ritual. The thing that makes this product different from any other todo app is live.

### Phase 3 — Match how my life actually works

"Awaiting" state with nudge dates and the "what's next" prompt. Lens switching (You / Mom). Ambient task re-surfacing integrated into the suggestion engine.

**Value at end of phase:** Feature-complete for v1. I can run my actual life through it, including Mom's stuff, and no-deadline tasks don't disappear.

### Phase 4 — Make it feel right and use it for real

Mobile-responsive layout. Visual design (palette, type, spacing). Daily use. Show one human (probably Mom) and watch them use it. Fix what breaks. Write a short retro.

**Value at end of phase:** I want to look at it. I'm using it daily. I have evidence from someone who isn't me.

Anything from previous-direction work that doesn't serve this plan should be archived or deleted, not preserved.

---

## What v1 success looks like

- You've stopped reaching for the notebook
- Your job-search prep lives inside the tool
- Mom's tasks are managed through the same app, separate lens
- The AI proposes today's picks each morning and you trust them enough to mostly accept
- One human who isn't you has used the lens and given feedback you acted on

## Open questions parked for now

- Name
- Visual aesthetic
- Whether to ever ship publicly

## Rules of the road

- Daily commits keep momentum. Even on a bad day, ship one small change (cosmetic, copy, docs).
- The PM agent guards the phase plan above. If you drift, it surfaces it. Listen.
- Each phase must end in something usable. If a phase is about to close without delivered value, stop and address that first.
- Daily log entry in README.md continues as before
