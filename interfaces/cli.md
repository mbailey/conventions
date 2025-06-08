# CLI Design Standards

## CLI Script Requirements

- Language: Prefer bash or python
- Documentation: Usage in `-h,--help`. Inline comments. `docs/scriptname.md`
- Input:
  - Argument parsing: Always include `-h,--help`
  - Scripts that accept input from a file should also accept it from STDIN
  - Shell completion
- Output:
  - Default to TSV output where script outputs columnar data
  - Default to stdout / stderr
  - TSV output should use "columnise" pattern when STDOUT is a terminal

## Code Style

- Use 4 spaces for indentation
- Do not include extensions for executables (.sh, .py, etc)
  - This enables changing the implementation language without affecting calling scripts
  - Scripts should have appropriate shebang lines to indicate their interpreter
  - Keeps command names clean and focused on their purpose rather than implementation

## CLI Coloured Output

- Use a consistent set of colours (and possibly emoji) for output
- Colours chosen should highlight different types of output as relevant to the program.
- Tools must respect the `NO_COLOR` environment variable by disabling all colored output when this variable is present (regardless of its value). See [no-color.org](https://no-color.org/) for the standard.

## CLI Prompts

- Use a consistent style for prompts requiring user response
  - Confirmation prompts:
    - Single item: `"(Y)eah/(N)ah/(A)bort/(D)on't ask again [YEAH]:"`
    - One of multiple items: `"(Y)eah/(N)ah/(A)ll/(Q)uit/(D)on't ask again [YEAH]:"`