# Roadmap

## M0 - Scaffold (this folder)
- [x] Data converted to JSON (parameters, principles, matrix)
- [x] CLAUDE.md, SPEC.md, worked examples
- [ ] `npm create vite@latest` (vanilla), wire `data/` imports

## M1 - Core library
- [ ] `src/triz.js`: `lookup`, `getPrinciples`, `searchParameters`
- [ ] Vitest: all 2304 cells vs. source, diagonal handling, directionality
- [ ] Load examples from `data/examples.json`

## M2 - Artifact prototype (single-file HTML)
- [ ] Wizard: Problem -> If/Then/But -> Mapping -> Matrix -> Principles
- [ ] Parameter picker with search and mapping tips
- [ ] Runner-up comparison
- [ ] Copy as Markdown
- [ ] Publish as Claude artifact

## M3 - AI assistance
- [ ] `src/ai.js` with `reframe`, `map`, `apply`
- [ ] Prompt templates + JSON schema validation
- [ ] Suggestion UI (accept / edit / reject)
- [ ] Backend proxy for the API key

## M4 - Web app
- [ ] Multi-contradiction sessions, bad-compromise field, comparison view
- [ ] Save/load (IndexedDB), export MD/JSON
- [ ] Onboarding with worked examples

## M5 - Workshop mode (stretch)
- [ ] Shared sessions, voting, facilitator view
- [ ] i18n EN/FR/NL
