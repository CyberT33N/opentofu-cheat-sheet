# fmt

[INTENT: REFERENCE]

Reformat your configuration in the standard style.

## Usage

```shell
tofu fmt [options] [target...]
```

## Options

- `-list=false` — do not list files whose formatting differs (always disabled when using STDIN).
- `-write=false` — do not write to source files (always disabled when using STDIN or `-check`).
- `-diff` — display diffs of formatting changes.
- `-check` — check if the input is formatted; exit status `0` if all input is properly formatted, non-zero otherwise.
- `-recursive` — also process files in subdirectories (by default only the given or current directory is processed).
- `-no-color` — disable colored output.

## Architectural explanation

`fmt` rewrites all OpenTofu configuration files to the canonical format: `.tf`, `.tofu`, `.tfvars`, `.tftest.hcl` and `.tofutest.hcl` files are processed; JSON variants (`.tf.json`, `.tfvars.json`, `.tftest.json`) are not modified. Targets can be directories, single files, or `-` for standard input. Content must be in the native OpenTofu language syntax; JSON is not supported. With `-check` the command is read-only and acts as the formatting gate for CI — verified in the state-home quality gate, where the check covered a `.tofutest.hcl` behavioral-proof file alongside the `.tf` files.

## Verified example

```shell
tofu fmt -check -diff -recursive
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: exit status `0` with no output — all configuration files (root module, child module, test file) already matched the canonical format.

## Troubleshooting & verified behavior details

- **`-diff` requires an external `diff` executable in `PATH`.** On Windows without a `diff` tool, `tofu fmt -check -diff -recursive` fails with exit status `2` and `Error: Failed to generate diff ... exec: "diff": executable file not found in %PATH%`. The failure only surfaces when at least one file actually differs — a fully formatted tree exits `0` without ever invoking `diff`. Verified on OpenTofu v1.12.5 (windows_amd64) with intentionally unformatted `.tf`, `.tofu`, and nested module files.
- **The exact `-check` exit status is `3`** when files differ from the canonical format (upstream documents only "non-zero"); the output lists the affected file paths, correctly excluding `.tf.json` files and including `.tofu` files. Verified on OpenTofu v1.12.5 (windows_amd64).
- **`-write=false` without `-check` renders the formatted content to stdout** instead of modifying files (verified in the default non-recursive scope: files in subdirectories are neither written nor rendered). Combined with `-list=false`, no file list is printed.
- **STDIN mode:** piping content into `tofu fmt -` prints the formatted result to stdout and never writes files; `-list` and `-write` are always disabled in this mode. Verified on OpenTofu v1.12.5 (windows_amd64).
- **JSON boundary re-verified through a write pass:** a deliberately unformatted `config.tf.json` remained byte-identical after `tofu fmt -recursive`, while the `.tf`, `.tofu`, and nested `.tf` files were rewritten; a subsequent `tofu fmt -check -recursive` returned exit status `0`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
