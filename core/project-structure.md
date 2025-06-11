# Project Structure Standards

## Software Projects

- Software projects always exist in a git repository.
- A project may include a module or a package.

### Modules

- A module is a project structure that may contain multiple packages.
- Modules keep each package in a dir (e.g. `my_package`) located in repo_root or a subdir (e.g. `packages/my_package`).

### Packages

A package has no dependencies on a module and can be extracted out into a
standalone project.

#### Package Layout

- README.md
- docs/
  - somescript.md
- bin/
  - somescript # Scripts should not have file extensions
- data/ # Git Ignored
- config/ # Provide full path to target location
  - HOME/ # Replaced with $HOME
    - dot-config/ # translates to `.config`
      - somescript.yml
  - etc/ # example of config that is deployed to root dir
    - logrotate.d/
      - somescript
- lib/
  - somelib.sh
  - somelib.py
- libexec/ # Optional
- shell/
  - env
  - path # Used by metool to manipulate path. format="path/to/dir [append/prepend/remove]"
  - functions/ # Sourced by metool so available from terminal
  - completions/
    - bash/
    - zsh/
- prompts/ # AI prompts and templates (organize as needed)
- test/ # prefer bats tests to test CLI tools
- vendor/

## Packages provide common interface for standard tasks

Each package should provide a standard interface for common tasks.
This means users do not need to remember the commands (such as pytest, bats, go build, etc).
The should only be included where relevant.

- **bin/test**: Run the tests (which may be pytest, bats, etc).
- **bin/build**: If there is a need to build (e.g. golang).
- **bin/install**: If it needs to be installed on local device.
- **bin/deploy**: Where there is a need to deploy to remote environments.

## Prompts Organization

### Package-Level Prompts

- Store source prompts in `prompts/` directory within each package
- Organize subdirectories as makes sense for your use case
- Use symlinks from config directories to maintain package cohesion
- Example: `config/dot-claude/commands/commit.md -> ../../../prompts/commit.md`

### Central Prompts Collection

- Use `packages/prompts/` as a central catalog via symlinks
- Structure: `packages/prompts/PACKAGE/ -> ../PACKAGE/prompts/`
- Provides discoverability while maintaining package independence
- Enables standalone distribution of prompt collections

### Benefits

- **Co-location**: Prompts live with related tools and documentation
- **Reusability**: Same prompts accessible from multiple contexts
- **Version Control**: Source files properly tracked without duplication
- **Distribution**: Packages remain self-contained for independent sharing

## External Repositories

- Manage external git repositories using `mt sync` with repos.txt
- Store external repos in `external/` directory
- Document each external dependency in repos.txt with purpose comment
- Prefer native binaries over containers when reasonable for performance
