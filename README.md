# /add-innovation

Your codebase already contains the next great feature. You just can't see it yet.

Two Claude Code commands that read your project — structure, docs, git history, actual source — and surface the single highest-leverage thing hiding in plain sight. Not "add dark mode." Not "improve logging." The thing that makes someone say *"why didn't we think of this before?"*

One winner. No menus. No hand-waving.

## Two lanes

**`/add-innovation`** — dream big.
What could this project *become*? Generates 5 moonshots, kills the boring ones, picks the most exciting survivor, and hands you a weekend experiment to validate it. Feasibility is not a filter — coherence is.

**`/add-based-innovation`** — discover what's already there.
Your repo has data flows, interfaces, and patterns that compose into something bigger than their original purpose. This finds that composition and proves it file by file — 3+ repo anchors, zero critical unknowns, or no winner.

```
/add-innovation                     → "holy shit, great idea — let's explore this"
/add-based-innovation               → "wait — we can already do this?"
```

## Get started

```bash
# Just drop the commands in
cp commands/add-innovation.md ~/.claude/commands/
cp commands/add-based-innovation.md ~/.claude/commands/
```

Then open any project and type:

```
/add-innovation
```

Watch it read your codebase and come back with something you didn't expect.

Focus it with an argument:

```
/add-innovation AI features
/add-based-innovation performance
```

## Under the hood

Both lanes start with a deep read of your project. Then they diverge:

```
                ┌─ stretch ─────────────────────────────────┐
 Read project → │  5 moonshots → coherence critique →       │
 Build map ─────┤  conviction vote → winner + experiment    │
                ├─ production ──────────────────────────────┤
                │  5 candidates → self-critique → evidence  │
                │  gate (3+ anchors) → winner + blueprint   │
                └───────────────────────────────────────────┘
```

## What it won't do

- Suggest "better logging", "more tests", or "add documentation"
- Recommend something generic that could apply to any project
- Give you a list of 5 options and say "pick one"
- Force a winner when nothing qualifies

## License

MIT
