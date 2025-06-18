# AI Entrypoints

Minimal configuration files that instruct AI coding assistants to read your project conventions.

## Setup

This conventions repository should be cloned into your project at `.conventions/`:

```bash
cd your-project
git clone https://github.com/mbailey/conventions .conventions
```

Then add the conventions to your AI tool configuration:

### Option 1: Append to Existing Config (Recommended)

If you already have project-specific AI instructions:

```bash
# Append conventions to your existing CLAUDE.md
echo -e "\n" >> CLAUDE.md  # Add newline separator
cat .conventions/ai-entrypoints/claude/CLAUDE.md >> CLAUDE.md

# For other tools (coming soon)
cat .conventions/ai-entrypoints/cursor/cursor-rules.md >> .cursorrules
```

### Option 2: Symlink (For New Projects)

If you don't have existing AI configuration:

```bash
# Symlink for Claude
ln -s .conventions/ai-entrypoints/claude/CLAUDE.md CLAUDE.md

# For other tools (coming soon)
ln -s .conventions/ai-entrypoints/cursor/cursor-rules.md .cursorrules
```

## Directory Structure

```
ai-entrypoints/
├── claude/
│   ├── CLAUDE.md         # Main Claude configuration
│   └── CLAUDE-voice.md   # Voice-specific Claude config
├── cursor/               # Coming soon
└── copilot/              # Coming soon
```

## Design Philosophy

These entrypoint files are intentionally minimal (just 3 lines). They simply:
1. Point the AI to `.conventions/CONVENTIONS.md`
2. Mention context-aware loading to reduce token usage

All actual convention content lives in the main conventions files, not in these entrypoints. This keeps token usage low and maintains a single source of truth.

## Integration Examples

### Example: Existing CLAUDE.md

If your project already has:
```markdown
# Project-Specific Instructions

- Always use async/await instead of promises
- Follow our custom error handling pattern
- Use our internal API client library
```

After appending conventions:
```markdown
# Project-Specific Instructions

- Always use async/await instead of promises
- Follow our custom error handling pattern
- Use our internal API client library

# Project Conventions

Read `.conventions/CONVENTIONS.md` for engineering standards and navigation instructions.

This project uses context-aware convention loading to minimize token usage.
```

### Example: New Project

For a new project without existing AI configuration:
```bash
# Just symlink the minimal entrypoint
ln -s .conventions/ai-entrypoints/claude/CLAUDE.md CLAUDE.md
```

The AI will automatically read your conventions while keeping token usage minimal.