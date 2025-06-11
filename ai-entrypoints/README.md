# AI Entrypoints

This directory contains entrypoint files for various AI coding assistants. These files instruct AI tools to read and follow the conventions defined in this repository.

## What Are These Files?

Each file is designed to be the first thing a specific AI assistant reads when working on your project. They all serve the same purpose: pointing the AI to your `CONVENTIONS.md` file.

## How to Use

1. **Symlink** the appropriate file into your project:
   ```bash
   ln -s ~/conventions/ai-entrypoints/CLAUDE.md .claude/CLAUDE.md
   ```

2. **Copy and customize** for project-specific needs:
   ```bash
   cp ~/conventions/ai-entrypoints/CLAUDE.md .claude/CLAUDE.md
   # Then add project-specific instructions
   ```

3. **Include the contents** in your existing AI configuration files

## Available Entrypoints

- `CLAUDE.md` - For Claude (Anthropic)
- More coming: cursor-rules.md, copilot.md, etc.

## The Pattern

All entrypoint files follow the same basic pattern:
1. Instruct the AI to read `CONVENTIONS.md`
2. Explain the context-aware loading system
3. Remind about checking for overrides

This ensures consistent behavior across different AI tools while respecting your personal conventions.