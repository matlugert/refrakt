# add-innovation skill

**Evidence-gated innovation discovery for codebases.**

Ships two commands that analyze your codebase, generate high-leverage feature candidates, self-critique them, then **prove each one against the actual code** before recommending a winner.

It's the difference between "what if we added AI?" and "here's exactly how your existing `completion_history` table, `Formatter` interface, and tag hierarchy enable a velocity dashboard — and here are the 5 files to touch."

## Two commands, same core

| Command | Style | Best for |
|---------|-------|----------|
| `/add-innovation` | Lean and fast | Quick ideation sessions, rapid-fire exploration |
| `/add-based-innovation` | Deep and structured | Thorough analysis with calibrated scoring rubrics, structured candidate templates, winner thresholds, and scope estimates |

Both follow the same 5-phase process and hard evidence gate. The difference is ceremony: `add-innovation` is concise output, `add-based-innovation` adds detailed scoring rubrics, candidate format templates (Pitch/Mechanism/Compounds), a >= 15/25 winner threshold, and S/M/L scope estimation in the blueprint.

## What makes it different

Most brainstorming produces ideas that sound great and fall apart on contact with reality. Refrakt has a **hard evidence gate**: every candidate must have 3+ concrete repo anchors proving feasibility, with zero critical unresolved dependencies. No evidence, no winner. It will tell you "no qualified winner" rather than recommend something speculative.

The process:

```
Capability Map → 5 Candidates → Self-Critique → Evidence Gate → Winner + Blueprint
```

Each candidate is scored on 5 dimensions (leverage, feasibility, wow-factor, compounding value, evidence confidence). The self-improving loop catches novelty inflation and hidden assumptions before the evidence gate catches missing proof.

## Install

### As a Claude Code plugin (recommended)

```bash
claude plugin install mlugert/refrakt
```

This installs both `/add-innovation` and `/add-based-innovation`.

### As slash commands (manual)

Copy the command files to your Claude Code commands directory:

```bash
# Global (available in all projects)
cp commands/add-innovation.md ~/.claude/commands/add-innovation.md
cp commands/add-based-innovation.md ~/.claude/commands/add-based-innovation.md

# Project-only (available in one project)
cp commands/add-innovation.md .claude/commands/add-innovation.md
cp commands/add-based-innovation.md .claude/commands/add-based-innovation.md
```

### As skills (manual)

Copy the skill directories:

```bash
# Global
cp -r skills/add-innovation ~/.claude/skills/add-innovation
cp -r skills/add-based-innovation ~/.claude/skills/add-based-innovation

# Project-only
cp -r skills/add-innovation .claude/skills/add-innovation
cp -r skills/add-based-innovation .claude/skills/add-based-innovation
```

**Windows (PowerShell):**

```powershell
# Global commands
Copy-Item commands\add-innovation.md "$env:USERPROFILE\.claude\commands\"
Copy-Item commands\add-based-innovation.md "$env:USERPROFILE\.claude\commands\"

# Global skills
Copy-Item -Recurse skills\add-innovation "$env:USERPROFILE\.claude\skills\add-innovation"
Copy-Item -Recurse skills\add-based-innovation "$env:USERPROFILE\.claude\skills\add-based-innovation"
```

## Usage

```
/add-innovation                       # Fast: analyze project, find best addition
/add-innovation AI features           # Fast: focus on AI opportunities
/add-based-innovation                 # Deep: full analytical treatment
/add-based-innovation performance     # Deep: focus on performance innovations
```

## Output

Both commands produce 6 mandatory sections in a fixed order:

| Section | What it contains |
|---------|-----------------|
| **Capability Map** | 5-8 bullets: what the project does, its stack, frontier, and gaps |
| **Candidate Table** | 5 candidates scored across 5 dimensions (25-point scale) |
| **Critique Delta** | What changed after the self-improvement cycle |
| **Evidence Ledger** | Repo anchors, proof statements, unresolved deps, PASS/FAIL per candidate |
| **Winner** | One winner (or explicit "no qualified winner") with justification |
| **Implementation Blueprint** | Files to touch, interfaces, data flow, edge cases, rollout plan |

`/add-based-innovation` adds to each section: detailed scoring rubric tables, structured candidate format (Pitch/Mechanism/Compounds), winner threshold (>= 15/25), and S/M/L scope estimation.

See [examples/sample-output.md](examples/sample-output.md) for a complete example of the deep variant.

## Scoring dimensions

| Dimension | What it measures |
|-----------|-----------------|
| **Leverage** | How much does this amplify the project's overall impact? |
| **Feasibility** | How buildable is this with what exists today? |
| **Wow-factor** | How surprising and delightful is this? |
| **Compounding value** | How much does this make existing capabilities more valuable? |
| **Evidence confidence** | How well-grounded is this in the actual codebase? |

Each scored 1-5. Full rubric (used by `/add-based-innovation`) in [skills/add-based-innovation/scoring-rubric.md](skills/add-based-innovation/scoring-rubric.md).

## Design principles

- **Evidence over enthusiasm.** Ideas are cheap. Proof is expensive. Refrakt requires proof.
- **One winner, not a menu.** Decision fatigue kills innovation. You get one recommendation or none.
- **Accretive, not additive.** Good features make existing features more valuable. Bolt-ons are banned.
- **No hygiene.** "Better logging", "more tests", "add docs" are not innovations.
- **Concrete, not hand-wavy.** "AI-powered insights" without a mechanism is auto-rejected.

## How it works internally

```
Phase A: Read project reality (structure, docs, git history, source)
         |
Phase B: Generate 5 candidates (accretive, feasible, non-obvious, compelling)
         |
Phase C: Self-critique all 5 (hidden assumptions, novelty inflation, dep risk)
         Revise once. Track the delta.
         |
Phase D: Evidence gate each candidate (3+ repo anchors, 0 critical deps)
         Hard gate: no evidence = no pass. No exceptions.
         |
Phase E: Pick one winner. Output implementation blueprint.
         Or: "No qualified winner" + next evidence-collection steps.
```

## FAQ

**Q: Which command should I use?**
A: Start with `/add-innovation` for quick sessions. Use `/add-based-innovation` when you want the full analytical depth — calibrated rubrics, structured templates, scope estimates.

**Q: What if no candidate passes the evidence gate?**
A: Both commands output "No qualified winner" with specific next steps. They never force a recommendation.

**Q: Does it work with any language/framework?**
A: Yes. Both commands read repo structure, docs, and source files. They work with any project that has source code.

**Q: Does it require internet access?**
A: No. All analysis is done against the local codebase.

## License

MIT
