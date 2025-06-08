# Project Structure Standards

## Software Projects

- Software projects always exist in a git repository.
- A project may include a module or a package.

### Modules

- A module is a project structure that may contain multiple packages.
- Modules keep each package in a dir, in repo_root or a subdir (e.g. `modules/`).

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

## External Repositories

- Manage external git repositories using `mt sync` with repos.txt
- Store external repos in `external/` directory
- Document each external dependency in repos.txt with purpose comment
- Prefer native binaries over containers when reasonable for performance