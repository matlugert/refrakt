# add-innovation skill

Your codebase already contains the next great feature. You just can't see it yet.

Refrakt reads your project — the structure, the docs, the git history, the actual source — and finds the single highest-leverage thing hiding in plain sight. Not "add dark mode." Not "improve logging." The thing that makes someone say *"why didn't we think of this before?"*

One winner. No menus. No hand-waving.

## Two lanes, pick your speed

**`/add-innovation`** — the stretch lane.
Dream big. What could this project *become*? Generates 5 moonshots, kills the boring ones, picks the most exciting survivor, and gives you a weekend experiment to validate it. Feasibility is not a filter — coherence is.

**`/add-based-innovation`** — the production lane.
Ship smart. What should you *actually build next*? Same 5 candidates, but every one must prove itself against your actual code — 3+ repo anchors, zero critical unknowns. No evidence, no winner. You get a complete implementation blueprint or an honest "nothing qualifies yet."

```
/add-innovation                     → "holy shit, we could do THAT?"
/add-based-innovation               → "here's exactly how to build it"
```

## Try it

```bash
# Install (Claude Code plugin)
claude plugin install mlugert/refrakt

# Or just drop the commands in
cp commands/add-innovation.md ~/.claude/commands/
cp commands/add-based-innovation.md ~/.claude/commands/
```

Then open any project and run:

```
/add-innovation
```

That's it. Watch it read your codebase and come back with something you didn't expect.

Want to narrow the focus? Pass an argument:

```
/add-innovation AI features
/add-based-innovation performance
```

## How it works

Both lanes start the same way — a deep read of your project to build a capability map. Then they diverge:

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
