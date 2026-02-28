# Refrakt Scoring Rubric — Detailed Guide

This rubric expands on the 5-dimension scoring system. Use this reference when calibrating scores across candidates.

## Leverage (1-5)

How much does this candidate amplify the project's overall impact?

| Score | Description | Example |
|-------|-------------|---------|
| 1 | Marginal improvement to one narrow area | "Add a tooltip to the settings page" |
| 2 | Useful addition but limited blast radius | "Support CSV export for one data type" |
| 3 | Clear value-add that touches multiple areas | "Add a plugin system for one module" |
| 4 | Significant multiplier across the project | "Universal plugin system that extends all modules" |
| 5 | Force multiplier — changes the project's trajectory | "Turn a tool into a platform" |

**Calibration question**: If this shipped tomorrow, how many other features would become easier or more valuable?

## Feasibility (1-5)

How buildable is this with what exists today?

| Score | Description | Red flags |
|-------|-------------|-----------|
| 1 | Requires new infrastructure, language, or major dependency | New database, new language, new cloud service |
| 2 | Significant integration work with uncertain outcomes | Complex third-party API with rate limits, auth changes |
| 3 | Moderate work building on existing patterns | New module following established conventions |
| 4 | Straightforward extension of existing code | New endpoint using existing patterns |
| 5 | Builds directly on existing code with minimal new surface | Composing existing modules in a new way |

**Calibration question**: Could a developer who knows this codebase build this in 1-3 sessions without asking "but how do we...?"

## Wow-factor (1-5)

How surprising and delightful is this?

| Score | Description | Test |
|-------|-------------|------|
| 1 | Expected / obvious / table stakes | Every competitor has it |
| 2 | Reasonable next step | "Yeah, that makes sense" |
| 3 | Pleasantly surprising | "Oh, that's clever" |
| 4 | Genuinely innovative | "I hadn't thought of that" |
| 5 | Paradigm-shifting | "Why didn't anyone think of this before?" |

**Calibration question**: If you described this at a meetup, would people lean forward or nod politely?

**Warning**: Novelty inflation is the #1 scoring bias. A 5 should genuinely surprise domain experts, not just sound cool.

## Compounding Value (1-5)

How much does this make _existing_ capabilities more valuable?

| Score | Description | Signal |
|-------|-------------|--------|
| 1 | Standalone feature, no interaction with existing code | Could be a separate tool |
| 2 | Light interaction with one existing feature | Shares a data model |
| 3 | Enhances 1-2 existing features meaningfully | Existing features get new use cases |
| 4 | Network effect across multiple features | Each existing feature becomes more valuable |
| 5 | Makes everything else more valuable | Existing users get value without changing behavior |

**Calibration question**: Does this create value _only_ for new users, or does it retroactively improve the experience for existing users too?

## Evidence Confidence (1-5)

How well-grounded is this candidate in the actual codebase?

| Score | Description | Anchor quality |
|-------|-------------|----------------|
| 1 | Speculative, no clear integration path | "This could probably work with..." |
| 2 | Some anchors, but significant gaps | 1-2 anchors, unclear how they connect |
| 3 | Reasonable anchors, minor gaps | 3+ anchors, small unknowns remain |
| 4 | Strong anchors, clear integration path | 4+ anchors, mechanism is well-defined |
| 5 | Strongly grounded, could start building today | Every step maps to existing code |

**Calibration question**: If you handed this blueprint to a developer with no context, could they find everything they need in the codebase?

## Anti-patterns (Score 0 — Auto-reject)

These candidates should be killed, not scored:

- **Hygiene masquerading as innovation**: "Add comprehensive error handling" is maintenance, not innovation
- **Infrastructure worship**: "Migrate to microservices" is a means, not an end
- **Technology-first thinking**: "Use GraphQL" without explaining what it enables for users
- **Vague magic**: "AI-powered insights" without a specific mechanism
- **Bolt-on features**: Something that could be a separate tool and doesn't compound existing value
