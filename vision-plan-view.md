# Plan view — populated vision

_Designer sketch, 2026-06-04. Reference for future polish sessions. Not for current implementation._

## Context

This is the target state for Plan view when populated with realistic data (~4–5 goals, 20–30 tasks). Plan view is the manual review/edit surface for the task pile. Today view (Phase 2) is the home — Plan is where you go to reshape what Today proposes.

## The problem this solves

A flat scroll of ~28 identical white card rows separated by tiny chip pills gives the eye nothing to anchor on. Anita flagged this in the Session C live walkthrough (2026-06-04): _"current UI is going to make it very hard to manage a long list of to-do's, there is no visual element."_

## What the eye needs

1. **Goal boundaries** — where one section ends and the next begins.
2. **Goal identity at a glance** — which life area, how many tasks, how stale.
3. **Navigation without endless scrolling** — at 60+ tasks, scrolling alone breaks.

## Recommended direction (A): left-rail goal index + heavy section headers

```
┌─────────────────────────────────────────────────────────────────────┐
│  PLAN                                                  [You ▾]      │
├──────────────┬──────────────────────────────────────────────────────┤
│              │                                                      │
│  GOALS       │  ▌ Land next role                          CAREER    │
│              │  ▌ 5 tasks · touched 2d ago                          │
│  ● Land...   │  ─────────────────────────────────────────────────   │
│    5 · 2d    │   ○  Update LinkedIn headline                        │
│              │   ○  Draft outreach to Priya                         │
│  ● Mom's...  │   ○  Prep STAR stories                  awaiting     │
│    4 · 6d    │   ○  Research target companies                       │
│              │   ○  Refresh portfolio site                          │
│  ● Half...   │                                                      │
│    3 · 12d   │  ▌ Mom's care plan                          FAMILY   │
│              │  ▌ 4 tasks · touched 6d ago                          │
│  ● Garden    │  ─────────────────────────────────────────────────   │
│    8 · 1d    │   ○  Call Dr. Chen re: medication                    │
│              │   ○  Order pill organizer                            │
│  ─────────   │   ○  Set up grocery delivery            awaiting     │
│  STANDALONE  │   ○  Schedule home aide visit                        │
│    8         │                                                      │
│              │  ▌ Half marathon training                  HEALTH    │
│              │  ▌ 3 tasks · touched 12d ago  ⚠ stale                │
│              │  ─────────────────────────────────────────────────   │
│              │   ○  Book physio appt                                │
│              │  ...                                                 │
└──────────────┴──────────────────────────────────────────────────────┘
```

## What's doing the work

- **Left rail = goal index (~140px).** Each goal shows title (truncated), task count, days-since-last-touch. Click jumps to section. This is the navigation answer; at 60+ tasks, scrolling alone breaks.
- **Goal section header is the anchor.** Thick left border (~3px), goal title in 18px semibold, category chip right-aligned, metadata line (`5 tasks · touched 2d ago`) below in 12px gray. Chapter-break visual weight.
- **Task rows drop the category chip when inside a goal section.** The header already states the category. Chips only on Standalone rows.
- **Status as right-edge label, not a chip.** `awaiting` in italic 12px gray, right-aligned. Quiet but always visible. Honors bet #4 ("awaiting feels held, not lost").
- **Staleness on goals, not tasks.** `⚠ stale` next to metadata line when `touched > 10d ago`. Maps to brief's "goals that haven't moved" Today-view signal.

## Alternatives considered

**Direction B — Collapsible goal sections, no rail.** Simpler DOM, mobile-native, but hides the pile (the whole point of Plan view) and re-opening every session is friction.

**Direction C — Density toggle (compact / comfortable) with current flat layout.** Minimal change but doesn't solve the anchor problem — a denser wall of white is still a wall.

## Stepping stone for the next polish session

Build just the **heavy goal section header** (3px left border, bigger semibold title, metadata line). ~60% of the hierarchy at low implementation cost, and a natural prerequisite for the full rail.

## Explicit non-goals (do not absorb into v1)

- No drag-and-drop reordering.
- No animated collapse/expand for the rail itself in v1.
- No category filters in the rail — categories are for awareness, not navigation (bet #7).
- No Today-view-style polish leaking into Plan view (Today is the centerpiece; Plan stays honest and usable).

## Mobile

The rail collapses to a sticky goal dropdown at the top of the scroll. Same data, different surface. Phase 4 work.
