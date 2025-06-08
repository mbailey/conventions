# Python Conventions

## Script Interpreters

- Python: `#!/usr/bin/env python`

## Python Standards

- Use well thought out colours for terminal output

## Script Path Resolution

### Python Scripts

When needed, Python scripts should use native Python libraries for path resolution:

```python
# Get absolute path to script directory
import os
import sys
from pathlib import Path

# Path to the script itself
SCRIPT_PATH = os.path.abspath(__file__)
SCRIPT_DIR = os.path.dirname(SCRIPT_PATH)
```

This pattern:

- Resolves symlinks to find the true script location
- Enables reliable relative path references to project resources
- Works consistently regardless of how or where the script is called from
- Provides standardized path variables for use in scripts:
  - SCRIPT_PATH: Full path to the actual script file
  - SCRIPT_DIR: Directory containing the script

All scripts should use these resolved paths when referencing project files rather than assuming relative paths will work from the current directory.

## Python Package Management with uv

[uv](https://github.com/astral-sh/uv) is a modern Python package management tool designed to replace multiple traditional tools, including pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv, and more.

### Why use uv

- **Speed**: uv is dramatically faster than traditional Python tools
- **Simplicity**: One tool replaces many others, simplifying the Python workflow
- **Reproducibility**: Robust dependency resolution and lockfile support
- **Portability**: Works across Linux, macOS, and Windows/WSL

### Key Features

- **Environment Management**: Install and manage Python versions
- **Package Management**: Install, update, and remove dependencies
- **Script Running**: Run Python scripts with automatically managed dependencies
- **Dependency Resolution**: Lock dependencies for reproducible builds
- **Tool Execution**: Run tools without installation using `uvx`

### Common Commands

- **Install a Python version**: `uv python install 3.12`
- **Create a virtual environment**: `uv venv`
- **Install packages**: `uv pip install <package>`
- **Run scripts with dependencies**: `uv run script.py --with requests`
- **One-off tool execution**: `uvx cowsay "Hello"`

### Recommended Practices

- Use `uv run` for script execution with dependency management
- Use `uvx` for one-off tool usage without permanent installation
- Use inline script metadata for declaring script dependencies
- Lock dependencies for reproducible environments

### Documentation

For more detailed information, see the [uv documentation](https://docs.astral.sh/uv/) and our local resources:

- [Running scripts with uv](/packages/uv/Running_scripts_uv.md)
- [uv vs uvx comparison](/packages/uv/docs/uv-vs-uvx.md)
- [uv README](/packages/uv/README.md)