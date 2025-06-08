# Core Engineering Principles

## General Principles

- Principle of Least Surprise.
- Make it as simple as possible, but no simpler.
- Ideally, code should be portable:
  - Linux: debian/ubuntu, fedora/redhat
  - macOS: Recent versions of Apple's OS. Optimised for Apple Silicon where appropriate.
  - WSL: Windows Subsystem for Linux

## Making Changes

When modifying code, especially user interfaces or command behavior, always review and update these related components:

- Tests - Update or add tests to cover the new behavior
- Documentation - Update relevant README files and docs/ directory content
- Shell completion - Update completion scripts to reflect new commands/options
- Configuration examples - Update example config files if config options changed
- Help/usage text - Update -h/--help output to match new behavior

Review changes holistically to maintain consistency across all project components.

## Organization

- Lists of items (including functions within files) should be alphabetized unless a different ordering is more appropriate for the context

## Naming Conventions

- Use short names but descriptive names
- Use `kebab-case` for file names
  - Special case: README files should always be capitalized as `README.md`
- Use `snake_case` for function names and variables
- Do not include file extensions on executable scripts
- Use Big Endian naming for files and functions
- Commands (files and functions) should be named like this:
  - Pluralised noun for listing items: `files`, `buckets`
  - noun-noun for listing related items or properties: `bucket-owner`, `file-properties`
  - noun-verb for acting on items: `file-create`, `file-delete`

This naming pattern enables better command discovery through tab completion. Users can:

1. Type a noun (e.g., 'instance') and press TAB to see all available operations for that resource
2. Discover related resources through noun-noun relationships
3. Build intuitive pipelines that flow from resource selection to action

For example, these command pipelines become natural to discover and read:

```bash
# List web instances and terminate them
instances | grep web | instance-terminate

# Find instances in a stack and delete their stack
instances | grep api | instance-stack | stack-delete
```

Compare this to verb-first naming where `delete-*` would show all deletable resources,
making it harder to discover operations available for a specific resource type.

### Examples of Command Pipelines

```bash
# Find all production instances and list their IPs
instances | grep prod | instance-ip

# List all buckets and their sizes
buckets | bucket-size

# Find instances in a region and show their security groups
instances | grep us-west-2 | instance-security-groups
```