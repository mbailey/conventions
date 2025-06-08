# Dependency Management

## Dependency Principles

- Minimise use of external dependencies.
- Follow conventions for dependency management: e.g. requirements.txt for python
- Scripts should list dependencies in the comments at the top
- Scripts should check that dependencies are present and if not, offer to install.

## External Repositories

- Manage external git repositories using `mt sync` with repos.txt
- Store external repos in `external/` directory
- Document each external dependency in repos.txt with purpose comment
- Prefer native binaries over containers when reasonable for performance