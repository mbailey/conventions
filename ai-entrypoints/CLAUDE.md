# Claude Integration

## Primary Directive

ALWAYS read CONVENTIONS.md at the start of any session to understand the engineering conventions for this project.

## Context-Aware Loading

Load specific convention modules based on the current work context:

- **Editing bash scripts**: Load `core/principles.md` + `languages/bash.md` + `interfaces/cli.md`
- **Python development**: Load `core/principles.md` + `languages/python.md` + `interfaces/cli.md`
- **Writing documentation**: Load `core/principles.md` + `core/documentation.md` + `languages/markdown.md`
- **General project work**: Load `CONVENTIONS.md` + `core/project-structure.md`

## Override System

Check for convention overrides in this order:
1. `conventions/` - Base conventions
2. `conventions-project/` - Project-specific overrides (if exists)
3. `conventions-local/` - Local personal overrides (if exists)

Later files override earlier ones for the same convention.

## Important Notes

- These conventions are personal preferences, not rigid rules
- Adapt suggestions to fit the specific project context
- When in doubt, ask for clarification rather than assume