# My Engineering Conventions

A personal collection of engineering conventions I use in my projects. I'm sharing these publicly as an example of how documenting your own conventions can significantly improve your experience with AI coding assistants.

## Why I'm Sharing This

1. **AI Coding Example**: This demonstrates how having well-documented conventions helps AI assistants understand your preferences and produce code that matches your style
2. **Maybe Useful Patterns**: Some of these patterns might be useful to others - feel free to adopt, adapt, or ignore as you see fit

## No Guarantees

These are my personal preferences that work for me. They may not work for you. Use at your own discretion.

## What's Here

- 📋 **My Standards**: How I structure projects, name things, design CLIs, test, and document
- 🔧 **Override System**: A pattern I use to customize conventions per-project without losing the base
- 🤖 **AI-Friendly**: Organized for context-aware loading by AI assistants
- 📦 **Templates**: Script templates I use regularly
- 🔗 **Integration Patterns**: Ways I've found to integrate these into projects

## Quick Start

### Clone into Your Project

```bash
# Navigate to your project
cd your-project

# Clone conventions as a subdirectory
git clone https://github.com/mbailey/conventions .conventions

# Add conventions to your AI assistant config
# Option 1: Append to existing CLAUDE.md (recommended)
echo -e "\n" >> CLAUDE.md
cat .conventions/ai-entrypoints/claude/CLAUDE.md >> CLAUDE.md

# Option 2: Symlink if no existing config
ln -s .conventions/ai-entrypoints/claude/CLAUDE.md CLAUDE.md

# Or browse .conventions/ and cherry-pick what you like
```

### For AI Assistants

The `ai-entrypoints/` directory contains minimal configuration snippets for different AI tools. These 3-line files simply point the AI to read `.conventions/CONVENTIONS.md` for all convention details:

- **Claude**: Append `.conventions/ai-entrypoints/claude/CLAUDE.md` to your project's CLAUDE.md
- **Cursor**: Coming soon
- **GitHub Copilot**: Coming soon

The AI assistant will read the conventions and use context-aware loading to minimize token usage. Since the entrypoint is only 3 lines, it integrates cleanly with your existing project-specific AI instructions.

## What's Included

### Core Stuff
- **[Principles](core/principles.md)**: How I think about naming things and organizing code
- **[Project Structure](core/project-structure.md)**: How I lay out packages and modules
- **[Documentation](core/documentation.md)**: My documentation habits
- **[Testing](core/testing.md)**: How I approach testing
- **[Dependencies](core/dependencies.md)**: How I manage dependencies

### Language-Specific
- **[Bash](languages/bash.md)**: My shell scripting patterns
- **[Python](languages/python.md)**: Python conventions I follow (I really like uv)
- **[Markdown](languages/markdown.md)**: How I format documentation

### Interface Design
- **[CLI Design](interfaces/cli.md)**: How I design command-line interfaces
- **[Configuration](interfaces/configuration.md)**: Config patterns that work for me
- **[Output Formatting](interfaces/output-formatting.md)**: Consistent output (TSV by default!)

## My Override System

This is a pattern I use to customize conventions per-project without losing the base:

```
.conventions/             # Base conventions (this repo, cloned into project)
conventions-project/      # Project-specific overrides (committed)
conventions-local/        # My local tweaks (gitignored)
```

Example: When a project needs different Python conventions:

```bash
# Create project-specific Python standards
mkdir -p conventions-project/languages
cat > conventions-project/languages/python.md << 'EOF'
# This Project's Python Standards

- Use Python 3.11+
- Always use type hints
- Prefer pytest over unittest

# Base conventions still apply unless overridden
EOF
```

## How to Use These

### 1. As a Project Subdirectory (Recommended)
```bash
cd your-project
git clone https://github.com/mbailey/conventions .conventions

# Add to existing CLAUDE.md
echo -e "\n" >> CLAUDE.md
cat .conventions/ai-entrypoints/claude/CLAUDE.md >> CLAUDE.md
```

### 2. With External Repository Management
```bash
# I use metool for this
echo "_mbailey:mbailey/conventions " >> .repos.txt
mt sync
```

### 3. Just Copy What You Need
```bash
# Cherry-pick specific files
cp .conventions/templates/scripts/bash-template my-script
```

### 4. Fork and Make Your Own
If you like the structure but want different conventions, fork it and make it yours!

## Examples

### How AI Assistants Use These

When I tell Claude I'm working on different things, it loads different conventions:

```markdown
# When I'm editing bash scripts
Load: core/principles.md + languages/bash.md + interfaces/cli.md

# Python development  
Load: core/principles.md + languages/python.md + interfaces/cli.md

# Writing documentation
Load: core/principles.md + core/documentation.md + languages/markdown.md
```

### Using My Templates

```bash
# I start new bash scripts from my template
cp .conventions/templates/scripts/bash-template my-script
chmod +x my-script
# Then customize from there
```

## My Philosophy

- **Principle of Least Surprise**: I prefer the most obvious approach
- **Simplicity**: As simple as possible, but no simpler
- **Flexibility**: These are my guidelines, not gospel - you do you
- **Practicality**: Based on what's worked for me over the years

## Contributing

This is my personal collection, but if you spot errors or have suggestions, feel free to open an issue. I'm not looking to build a comprehensive standard - just sharing what works for me.

## License

GPL-3.0 - Because conventions and ideas should remain free.

---

*Remember: The best conventions are the ones you actually follow. These are mine. Yours will be different, and that's okay.*
