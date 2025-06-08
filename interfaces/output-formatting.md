# Output Formatting Standards

## TSV Output Standards

- Default to TSV output where script outputs columnar data
- Default to stdout / stderr
- TSV output should use "columnise" pattern when STDOUT is a terminal

## Use Columnise Pattern in CLI scripts that produce TSV output

The columnise pattern formats tabular data with aligned columns when output is
a terminal, but preserves TSV format when piping to another command.

```shell
columnise() {

  # Check if no arguments are provided
  if [ $# -eq 0 ]; then
    if ! [[-t 1]]; then
      cat
    else
      column -t -s $'\t'
    fi
  else
    # Loop through all arguments
    for file in "$@"; do
      if [ -e "$file" ]; then # Process the file if it exists
        column -t -s $'\t' < "$file"
      else # Print an error message if the file doesn't exist
        echo "Error: File '$file' does not exist" >&2
      fi
    done
  fi
}
```

## Colored Output

- Use a consistent set of colours (and possibly emoji) for output
- Colours chosen should highlight different types of output as relevant to the program.
- Tools must respect the `NO_COLOR` environment variable by disabling all colored output when this variable is present (regardless of its value). See [no-color.org](https://no-color.org/) for the standard.

## User Prompts

- Use a consistent style for prompts requiring user response
  - Confirmation prompts:
    - Single item: `"(Y)eah/(N)ah/(A)bort/(D)on't ask again [YEAH]:"`
    - One of multiple items: `"(Y)eah/(N)ah/(A)ll/(Q)uit/(D)on't ask again [YEAH]:"`