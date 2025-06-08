# Convention Override System

This package supports a three-tier override system that allows teams and individuals to customize conventions without forking.

## Three-Tier Hierarchy

1. **Base conventions** (from conventions package)
2. **Project conventions** (team overrides, committed to git)
3. **Local conventions** (individual overrides, gitignored)

## Integration Patterns

### As Submodule (Recommended)

```bash
# Add as git submodule
git submodule add https://github.com/mbailey/conventions-package conventions

# Create symlink at project root
ln -s conventions/CONVENTIONS.md .

# Create project override directories
mkdir -p conventions-project
mkdir -p conventions-local

# Add to .gitignore
echo "conventions-local/" >> .gitignore
```

### As Copy (For Customization)

```bash
# Copy for heavy customization
cp -r conventions-package/* project/conventions/

# Create override directories
mkdir -p conventions-project
mkdir -p conventions-local
```

### Using External Repos (Metool Style)

```bash
# In external/repos.txt
_mbailey:mbailey/conventions-package conventions shared

# Run sync
mt sync external/

# This creates symlinks automatically
```

## Directory Structure

```
my-project/
├── conventions/                     # Base conventions (submodule or copy)
│   ├── CONVENTIONS.md
│   ├── core/
│   │   └── principles.md
│   └── languages/
│       ├── bash.md
│       └── python.md
├── conventions-project/             # Team overrides (committed to git)
│   ├── project-specific.md         # Additional project conventions
│   └── languages/
│       └── python.md               # Override base python.md
└── conventions-local/               # Individual overrides (gitignored)
    └── languages/
        └── python.md               # Personal overrides
```

## File Resolution Order

For any convention file (e.g., `languages/python.md`):

1. `conventions/languages/python.md` (base)
2. `conventions-project/languages/python.md` (team override, if exists)
3. `conventions-local/languages/python.md` (individual override, if exists)

## Creating Overrides

### Project-Level Override Example

```bash
# Create project-specific Python conventions
cat > conventions-project/languages/python.md << 'EOF'
# Project Python Conventions

## Our Specific Requirements

- Use Python 3.11+
- Always use type hints
- Use our custom logging framework

# Include base conventions
<!-- Base conventions still apply unless explicitly overridden -->
EOF
```

### Individual Override Example

```bash
# Personal preference for Python
cat > conventions-local/languages/python.md << 'EOF'
# My Personal Python Preferences

## Additional Tools
- Use black for formatting
- Use mypy for type checking

EOF
```

## AI Assistant Integration

Configure your AI assistant to load conventions in the correct order:

```markdown
# In CLAUDE.md
- Read conventions/CONVENTIONS.md (base)
- Read conventions-project/project-specific.md (if exists)
- For Python work:
  - Load conventions/languages/python.md
  - Load conventions-project/languages/python.md (if exists)
  - Load conventions-local/languages/python.md (if exists)
```

## Benefits

- **No Forking**: Customize without losing upstream updates
- **Team Consistency**: Share project conventions via git
- **Individual Flexibility**: Personal preferences stay local
- **Clear Hierarchy**: Easy to understand what overrides what
- **Git Friendly**: Clean separation of committed vs ignored content