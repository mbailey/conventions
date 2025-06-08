# Engineering Conventions

## Quick Reference

### Core Standards
- [Core Principles](core/principles.md) - General engineering principles and naming conventions
- [Project Structure](core/project-structure.md) - Package/module layout standards  
- [Documentation](core/documentation.md) - Documentation requirements and markdown standards
- [Testing](core/testing.md) - Testing conventions and requirements
- [Dependencies](core/dependencies.md) - Dependency management practices

### Language-Specific
- [Bash](languages/bash.md) - Shell scripting conventions
- [Python](languages/python.md) - Python development standards including uv
- [Markdown](languages/markdown.md) - Documentation formatting rules
- [Shell Completions](languages/shell-completions.md) - Completion script standards

### Interface Design
- [CLI Design](interfaces/cli.md) - Command-line interface patterns
- [Configuration](interfaces/configuration.md) - Config file and environment variable patterns
- [Output Formatting](interfaces/output-formatting.md) - TSV, colors, and user prompts

### Templates and Overrides
- [Templates](templates/) - Standardized templates for projects and scripts
- [Override System](overrides/README.md) - How to customize conventions for your project

## Essential Principles

- **Principle of Least Surprise** - Choose the most obvious approach
- **Simplicity** - Make it as simple as possible, but no simpler
- **Portability** - Support Linux (Debian/Ubuntu, Fedora/RedHat), macOS, and WSL
- **Consistency** - Follow established patterns within the project
- **Context-Aware Loading** - Load only relevant conventions based on work context

## Context-Aware Usage

Load specific convention modules based on your current work:

```bash
# Editing bash scripts
Load: core/principles.md + languages/bash.md + interfaces/cli.md

# Python development  
Load: core/principles.md + languages/python.md + interfaces/cli.md

# Writing documentation
Load: core/principles.md + core/documentation.md + languages/markdown.md

# General project work
Load: CONVENTIONS.md + core/project-structure.md
```

## Integration with Other Projects

This conventions package can be integrated into any project:

1. **As a submodule**: `git submodule add <repo> conventions`
2. **As external repo**: Add to `external/repos.txt` for metool sync
3. **As a copy**: For projects needing heavy customization

See [Override System](overrides/README.md) for detailed integration instructions.

## Making Changes

When modifying code, always review and update:
- Tests - Update or add tests to cover new behavior
- Documentation - Update README files and docs/ content
- Shell completion - Update completion scripts
- Configuration examples - Update example configs
- Help/usage text - Update -h/--help output

Review changes holistically to maintain consistency across all project components.