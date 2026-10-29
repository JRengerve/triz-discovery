# TRIZ Discovery

A guided tool for resolving contradictions (business, product, process, organizational) with the TRIZ 48-parameter Contradiction Matrix and the 40 Inventive Principles, with AI assistance for the judgment-heavy steps.

## Goal
1. **Phase 1 (artifact):** single-file HTML/JS prototype of the discovery wizard, publishable as a Claude artifact.
2. **Phase 2 (web app):** Vanilla JS + Vite app with saved sessions, export, and AI assistance via a thin backend proxy.

See `docs/SPEC.md` for the product spec and `docs/ROADMAP.md` for milestones.

## The core flow (do not change without discussion)
1. **Problem** - user describes the situation in plain language.
2. **If / Then / But** - restate as: If [change], Then [improving factor], But [worsening factor]. AI may propose reframings; the user confirms.
3. **Parameter mapping** - map Then -> improving parameter, But -> worsening parameter (1 of 48 each). Always show runner-up parameters and one-line reasoning. User can override.
4. **Matrix lookup** - exact lookup, row = improving, column = worsening. NOT symmetric. Diagonal cells are empty (handle gracefully: fall back to AI-suggested principles from definitions).
5. **Principles** - show 4-6 principles from the cell, each with the textbook definition AND a concrete, situation-specific application (AI-drafted, user-editable).
6. **Compare/export** - keep several contradictions per session, flag "bad compromises" the user wants to avoid, export as Markdown/JSON.

## Data (source of truth - verified)
- `data/parameters.json` - 48 parameters `{id, name, description}`
- `data/principles.json` - 40 principles `{id, name, description}`
- `data/matrix.json` - keys `"improvingId-worseningId"` -> array of principle ids (2304 cells, 48 empty on the diagonal)
- `data/examples.json` - worked examples from real sessions (use as test fixtures and onboarding demos)
- `docs/48-parameters.md` - includes mapping tips (cost is NOT a parameter: trace to 10, 41, 26 or 44)

Never hand-edit `matrix.json`. Spot-check: `32-41` -> `[10,13,29,31]`, `47-32` -> `[1,26,13,15]`, `24-26` -> `[3,14,28,15]`.

## Conventions
- Vanilla JS (ES modules), Vite, no framework. Plain CSS with variables. No localStorage in the artifact version (in-memory state); the web app may use localStorage/IndexedDB.
- Keep matrix/principles loading separate from UI (`src/triz.js` = pure functions: `lookup(improvingId, worseningId)`, `getPrinciples(ids)`), covered by unit tests (Vitest).
- AI calls go through one module (`src/ai.js`). In Phase 2, the API key lives on the server, never in the browser.
- AI output is a *suggestion*: always editable, always labelled, never silently overwrites user text.

## AI assistance guidelines
- Reframing: propose 2-3 If/Then/But variants, flag missing/ambiguous clauses (users often leave a clause truncated).
- Mapping: return best parameter + runner-up + one-line why. Use the mapping tips in `docs/48-parameters.md`.
- Applications: translate each principle into a concrete suggestion for the user's context; avoid restating the textbook definition.
- Encourage rejecting compromises: the point of TRIZ is to get both sides of the contradiction.

## Commands (once scaffolded)
- `npm install`, `npm run dev`, `npm test`, `npm run build`
