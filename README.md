# TRIZ Discovery

Guided tool to resolve contradictions with the TRIZ 48-parameter matrix and 40 inventive principles, with AI assistance.

## Getting started with Claude Code
```bash
cd triz-discovery
claude
```
Claude Code will read `CLAUDE.md`. Suggested first prompts:
1. "Read docs/SPEC.md and docs/ROADMAP.md, then scaffold M1 (Vite vanilla + src/triz.js + Vitest tests over all matrix cells)."
2. "Build the M2 single-file HTML prototype of the wizard using data/*.json and data/examples.json."

## Structure
```
CLAUDE.md          project instructions for Claude Code
data/              parameters, principles, matrix (JSON), worked examples
docs/              SPEC, ROADMAP, reference tables with mapping tips
src/               (to be created) triz.js, ai.js, UI
```

## Data
Matrix keys are `"improving-worsening"` (directional). Example: `matrix["32-41"] -> [10,13,29,31]`.
