# Configuration Standards

## Configuration Sources and Precedence

Configuration values should be readable from multiple sources, with the following precedence (highest to lowest):

1. Command line arguments
2. Environment variables
3. Configuration files

This allows for flexible usage while maintaining predictable override behavior.

## Command Line Arguments

- Use argparse library for Python implementations
- Always implement these standard arguments:
  - `-h, --help` - Show help/usage information
  - `-v, --version` - Show version information
  - `-c, --config` - Specify config file path
  - `-d, --verbose` - Output should be more verbose
  - `-d, --debug` - Enable debug output
- Provide both short (-x) and long (--xyz) forms for all arguments
- Prefer long-form arguments (--directory instead of -d) when they are portable across common Unix variants
- Use the GNU-style long options (--option) rather than BSD-style when available
- Short options should still be supported for interactive use
- Use consistent argument naming across related tools
- Always use long argument names when including commands in scripts

## Environment Variables

- Use UPPERCASE with underscores
- Prefix with application/tool name (e.g., MYTOOL_API_KEY)
- Document all supported environment variables in help output

## Configuration Files

- Support standard locations:
  - /etc/[toolname]/config
  - ~/.config/[toolname]/config
  - ./.[toolname]rc
- Use common formats (YAML, TOML, or INI)
- Document the config file format in examples