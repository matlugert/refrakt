# refrakt

**Evidence-gated innovation discovery for codebases.**

Refrakt takes your codebase, maps its capabilities, generates high-leverage feature candidates, self-critiques them, then **proves each one against the actual code** before recommending a winner with an implementation blueprint.

It's the difference between "what if we added AI?" and "here's exactly how your existing `completion_history` table, `Formatter` interface, and tag hierarchy enable a velocity dashboard — and here are the 5 files to touch."

## What makes it different

Most brainstorming produces ideas that sound great and fall apart on contact with reality. Refrakt has a **hard evidence gate**: every candidate must have 3+ concrete repo anchors proving feasibility, with zero critical unresolved dependencies. No evidence, no winner. It will tell you "no qualified winner" rather than recommend something speculative.

The process:

```
Capability Map → 5 Candidates → Self-Critique → Evidence Gate → Winner + Blueprint
```

Each candidate is scored on 5 dimensions (leverage, feasibility, wow-factor, compounding value, evidence confidence) with a detailed rubric. The self-improving loop catches novelty inflation and hidden assumptions before the evidence gate catches missing proof.

## Install

### As a Claude Code plugin (recommended)

```bash
claude plugin install mlugert/refrakt
```

### As a slash command (manual)

Copy the command file to your Claude Code commands directory:

```bash
# Global (available in all projects)
cp commands/refrakt.md ~/.claude/commands/refrakt.md

# Project-only (available in one project)
cp commands/refrakt.md .claude/commands/refrakt.md
```

### As a skill (manual)

Copy the skill directory:

```bash
# Global
cp -r skills/refrakt ~/.claude/skills/refrakt

# Project-only
cp -r skills/refrakt .claude/skills/refrakt
```

**Windows (PowerShell):**

```powershell
# Global command
Copy-Item commands\refrakt.md "$env:USERPROFILE\.claude\commands\refrakt.md"

# Global skill
Copy-Item -Recurse skills\refrakt "$env:USERPROFILE\.claude\skills\refrakt"
```

## Usage

```
/refrakt                          # Analyze entire project, optimize for leverage
/refrakt AI features              # Focus on AI/ML innovation opportunities
/refrakt developer experience     # Focus on DX improvements
/refrakt performance              # Focus on performance innovations
/refrakt new user segment         # Focus on reaching new users
```

## Output

Refrakt produces 6 mandatory sections in a fixed order:

| Section | What it contains |
|---------|-----------------|
| **Capability Map** | 5-8 bullets: what the project does, its stack, frontier, and gaps |
| **Candidate Table** | 5 candidates scored across 5 dimensions (25-point scale) |
| **Critique Delta** | What changed after the self-improvement cycle |
| **Evidence Ledger** | Repo anchors, proof statements, unresolved deps, PASS/FAIL per candidate |
| **Winner** | One winner (or explicit "no qualified winner") with justification |
| **Implementation Blueprint** | Files to touch, interfaces, data flow, edge cases, rollout plan |

See [examples/sample-output.md](examples/sample-output.md) for a complete example.

## Scoring dimensions

| Dimension | What it measures |
|-----------|-----------------|
| **Leverage** | How much does this amplify the project's overall impact? |
| **Feasibility** | How buildable is this with what exists today? |
| **Wow-factor** | How surprising and delightful is this? |
| **Compounding value** | How much does this make existing capabilities more valuable? |
| **Evidence confidence** | How well-grounded is this in the actual codebase? |

Each scored 1-5. Winner threshold: >= 15/25. Full rubric in [skills/refrakt/scoring-rubric.md](skills/refrakt/scoring-rubric.md).

## Design principles

- **Evidence over enthusiasm.** Ideas are cheap. Proof is expensive. Refrakt requires proof.
- **One winner, not a menu.** Decision fatigue kills innovation. You get one recommendation or none.
- **Accretive, not additive.** Good features make existing features more valuable. Bolt-ons are banned.
- **No hygiene.** "Better logging", "more tests", "add docs" are not innovations.
- **Concrete, not hand-wavy.** "AI-powered insights" without a mechanism is auto-rejected.

## How it works internally

```
Phase A: Read project reality (structure, docs, git history, source)
         ↓
Phase B: Generate 5 candidates (accretive, feasible, non-obvious, compelling)
         ↓
Phase C: Self-critique all 5 (hidden assumptions, novelty inflation, dep risk)
         Revise once. Track the delta.
         ↓
Phase D: Evidence gate each candidate (3+ repo anchors, 0 critical deps)
         Hard gate: no evidence = no pass. No exceptions.
         ↓
Phase E: Pick one winner. Output implementation blueprint.
         Or: "No qualified winner" + next evidence-collection steps.
```

## FAQ

**Q: What if no candidate passes the evidence gate?**
A: Refrakt outputs "No qualified winner" with specific next steps to collect missing evidence. It never forces a recommendation.

**Q: Can I change the number of candidates?**
A: The prompt is designed around 5 candidates as a sweet spot. Fewer limits diversity; more creates noise. You can fork and modify if needed.

**Q: Does it work with any language/framework?**
A: Yes. Refrakt reads repo structure, docs, and source files. It works with any project that has source code and some form of documentation.

**Q: Does it require internet access?**
A: No. All analysis is done against the local codebase. WebSearch is in the allowed tools list for optional context enrichment but is not required.

## License

MIT
