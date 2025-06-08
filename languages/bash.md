# Bash Conventions

## Script Interpreters

- Bash: `#!/usr/bin/env bash`

Rationale:

- Most unix executables don't have extensions.
- The language is an implementation detail that shouldn't impact the how to call it.

## Bash Standards

- Line 2 of bash scripts should contain: set -o nounset -o pipefail -o errexit

## Script Path Resolution

### When to Use Path Resolution

Include path resolution code ONLY when your script needs to:

- Access files relative to the script's location
- Reference resources in the project directory structure
- Work correctly when called via symlinks or from different directories

DO NOT include this code if your script:

- Doesn't reference any relative paths
- Only uses absolute paths or paths relative to the current working directory
- Doesn't need to locate its own directory

### Bash Scripts

When needed, bash scripts should include this path resolution code near the top:

```bash
# Get absolute path to script, even when called via symlink
command -v realpath &> /dev/null || {
    echo "Error: 'realpath' is required but not found. Please install 'coreutils' (e.g. 'brew install coreutils' on macOS)." >&2
    exit 1
}
SCRIPT_PATH="$(realpath "${BASH_SOURCE[0]}")"
SCRIPT_DIR="$(dirname "$SCRIPT_PATH")"
```

This pattern:

- Resolves symlinks to find the true script location
- Enables reliable relative path references to project resources
- Works consistently regardless of how or where the script is called from
- Provides standardized path variables for use in scripts:
  - SCRIPT_PATH: Full path to the actual script file
  - SCRIPT_DIR: Directory containing the script

All scripts should use these resolved paths when referencing project files rather than assuming relative paths will work from the current directory.