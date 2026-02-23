# Steelman

A Claude Code skill for pressure-testing decisions before you commit.

## What it does

When you invoke `/steelman`, Claude genuinely argues for the 2-3 strongest alternatives to whatever direction you've chosen. Not devil's advocate theater — real arguments, rooted in your specific context, presented at full strength. Then you decide whether to proceed, reconsider, or investigate further.

## Install

```
/install juandominguez/steelman
```

## Usage

State your direction, then invoke the skill:

```
"We're going with GraphQL for our API layer."
/steelman
```

Claude will:
1. **Name the blind spots** in your current choice
2. **Steelman 2-3 alternatives** — arguing each as if it's the better path
3. **Make an honest call** — did your choice survive the scrutiny, or is an alternative stronger?
4. **Present a decision prompt** — proceed, reconsider, or investigate

## When to use it

- Architecture choices (monolith vs. microservices, database selection)
- Technology selections (frameworks, languages, platforms)
- Business decisions (pricing models, go-to-market strategy)
- Any high-stakes choice where momentum bias might be doing the thinking for you

## Design principles

- **Anti-sycophancy** — no "your choice is still solid" retreats, no hedging, no false neutrality
- **Context over generics** — arguments use your specific situation, not textbook pros/cons
- **Conciseness** — one devastating argument beats five decent ones
- **Honest assessment** — if an alternative is stronger, Claude says so; if your choice wins, Claude says that too

## Built with TDD for skills

This skill was developed using the RED-GREEN-REFACTOR cycle from the [superpowers writing-skills](https://github.com/anthropics/claude-code-superpowers) methodology:

- **RED**: Baseline tested across 5 scenarios without the skill to identify failure patterns (sycophantic closings, no decision framework, missing "wins if" conditions, verbosity, no blind spot analysis)
- **GREEN**: Wrote skill addressing those specific failures, verified improvement
- **REFACTOR**: Added anti-sycophancy safeguards, effort-justification warnings, and false-neutrality detection through iterative testing

## License

MIT
