# Project Brief — v1

_30-day build challenge · brand-new coder · ~2 hours/day_
_Working name: TBD · Drafted day 0_

---

## What it is

A personal task system that thinks the way you do — built for you, by you, over 30 days. The upcoming job search is its first proving ground.

## The user

You. Mom-as-second-life is core to v1, not a stretch — multi-person is a v1 design constraint, not an afterthought.

## Why this and not another todo app

Your current setup (notebook + paper + Notepad) breaks in three specific places:

1. **Granularity** — aspirations ("learn piano") sit next to one-off calls ("call NY tax office") with no way to relate to either.
2. **Timeframe** — no good way to think about *when*.
3. **Follow-up** — things drop after the first action.

Off-the-shelf apps treat these as user errors. This one treats them as design problems.

## The opinionated bets

1. **Aspirations and tasks are different objects.** "Learn piano" is a goal that *generates* tasks (research digital pianos, find a teacher), not a task itself. Type is explicit at capture, or guessed and confirmed.
2. **Brain-dump in, structure out.** You type "piano/guitar" — the system asks one clarifying question ("Goal, or next action?") and shapes it.
3. **Categories for awareness, not just filtering.** Career / Finances / Health / Hobbies / Social / Home. The home view shows attention distribution across them.
4. **No-deadline tasks have a heartbeat.** "Custom bookshelf" re-surfaces every couple of weeks on its own. Visible without being overdue.
5. **Multiple lives are first-class.** A lens switcher between You and Mom. Same app, different worlds, separate data.
6. **"Awaiting" is a first-class state.** Many tasks aren't done when you mark them done — they're waiting on someone or something. The system models this explicitly: who you're waiting on, when to nudge you if nothing moves, and what the branching next steps are when input arrives. The system carries the *thread*, not just the *step*.

## In scope for day 30 — must-have core

- Brain-dump text capture with AI parsing into goals / tasks
- Category assignment (AI-suggested, you confirm)
- Ambient (no-deadline) vs. dated tasks, with re-surfacing logic for ambient
- "Awaiting" state — mark task as awaiting + who/when, auto-nudge on date, prompt for next step on resolve
- Lens switching between You and Mom (data model multi-person from day 1)
- Responsive web app — works in your phone browser and on desktop

## Stretch (cut first if days run short)

- Goals as parent objects with child tasks linked under them
- Job-search starter pack (pre-loaded category with template tasks)
- "Considering" parking lot for question-mark items, with weekly review prompt
- Branching follow-ups defined at capture time (the "if yes / if no / if no reply" structure)
- Category balance flagging ("Health has gone dark for two weeks")

## Deliberately out of scope

- Push notifications, native iOS app
- Sharing, collaboration, multi-user accounts
- Calendar sync, complex recurring schedules
- Import from any existing tool

## Stack

- Single-page web app — HTML / CSS / vanilla JS to start, React only if you outgrow it
- `localStorage` for v1 storage; add Supabase only if real cross-device sync becomes essential
- Claude API for the parsing layer
- Hosted on GitHub Pages or Vercel (free)
- VS Code as editor, Claude as pair programmer

## Day 30 looks like this

- You've stopped reaching for the notebook
- Your job-search prep lives inside the tool
- Mom's tasks are managed through the same app, separate lens
- One human who isn't you has seen it and given feedback you acted on

## Open questions parked for now

- Name
- Visual aesthetic
- Whether to ever ship publicly

## Rules of the road

- A day "counts" when something is shipped (committed to the repo, ideally pushed live)
- The minimum viable build for a bad day: one cosmetic or copy change, committed
- Use AI freely as a tutor and pair; type the first two weeks of code yourself to build instinct
- Keep a daily one-line log in the README: what shipped, what's stuck

