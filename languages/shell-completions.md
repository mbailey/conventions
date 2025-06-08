# Shell Completion Conventions

## Shell Completions

- Support bash completion across Linux variants and macOS
- Completion files should follow this pattern:
  - `shell/completions/[command-name]` for single command completion
  - `shell/completions/[project-name]` for project-wide completion
- Completion scripts should be documented in the project's README.md under Installation section

Example completion file structure:

```bash
shell/completions/
├── my-tool        # Project-wide completion
└── specific-cmd   # Single command completion
```