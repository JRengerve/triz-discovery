# Product Spec - TRIZ Discovery

## Problem
People facing trade-offs (product, business model, organizational) default to compromises. TRIZ offers a structured way out, but the 48x48 matrix and 40 principles are hard to use unaided, and the mapping step (real-world problem -> abstract parameter) is where most people stall.

## Users
- Innovation facilitators and workshop leads (e.g. portfolio/governance workshops)
- Product managers, founders, engineers exploring trade-offs
- Teams wanting a repeatable, documented way to explore options

## Core user journey
1. Describe a situation.
2. Get help restating it as If / Then / But; confirm.
3. Map both sides to TRIZ parameters (with reasoning, runner-ups, override).
4. See the matrix result and the principles.
5. Get concrete, context-specific applications per principle; edit/keep/discard.
6. Compare contradictions, note bad compromises to avoid, export.

## Features
### MVP (artifact)
- 5-step wizard, fully offline lookup (data embedded)
- Parameter picker with search, descriptions, mapping tips
- Result view: cell coordinates, principle cards (definition + user notes field)
- Runner-up lookup (swap alternative parameters, compare cells)
- Copy as Markdown

### V1 (web app)
- AI assistance (reframe, map, apply) via backend proxy
- Multiple contradictions per session; "bad compromise" field; side-by-side comparison
- Session save/load (local), export Markdown/JSON
- Shareable read-only session link (later)

### Later
- Workshop mode: shared board, voting on principles, facilitator prompts
- Principle browser with real-world examples, filters by domain (product, process, org, software)
- Library of worked examples (see `data/examples.json`)
- Reverse lookup: "which contradictions does principle #N usually resolve?"
- i18n (EN/FR/NL)

## Non-goals (for now)
- Full TRIZ toolkit (ARIZ, substance-field, trends of evolution) - possible later modules
- Auto-solving without user confirmation

## Key UX decisions
- Matrix is directional: label row "Improving" and column "Worsening" and never auto-swap.
- Empty cell (same parameter on both axes): explain why and offer principles from definitions.
- Show the mapping reasoning; the mapping step is where users need judgment, not magic.
- Business/org contradictions are first-class: ship mapping tips for them (e.g. "autonomy" -> 32 Adaptability, "visibility" -> 47 Ability to detect/measure, "sales output" -> 44 Productivity).

## Data model (session)
```json
{
  "id": "uuid",
  "title": "string",
  "problem": "string",
  "contradictions": [{
    "id": "uuid",
    "if": "string", "then": "string", "but": "string",
    "improving": 32, "worsening": 41,
    "runnerUps": { "improving": [], "worsening": [] },
    "badCompromise": "string",
    "principles": [{ "id": 10, "application": "string", "status": "keep|discard|undecided" }]
  }]
}
```

## AI integration
- Three prompts: `reframe`, `map`, `apply`. Structured JSON output; validate against parameter/principle ids before display.
- Provide the relevant slice of `parameters.json` / `principles.json` in the prompt; never ask the model to recall matrix cells (lookup is deterministic code).
- Phase 2: serverless/Node proxy holding the API key; rate limiting.

## Success criteria
- A first-time user goes from a plain-language problem to 4 concrete applications in under 10 minutes.
- Lookups match the verified matrix for every cell (automated test over all 2304 cells vs. CSV source).
