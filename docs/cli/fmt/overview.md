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

`fmt` rewrites all OpenTofu configuration files to the canonical format: `.tf`, `.tfvars`, and `.tftest.hcl` files are updated; JSON variants (`.tf.json`, `.tfvars.json`, `.tftest.json`) are not modified. Targets can be directories, single files, or `-` for standard input. Content must be in the native OpenTofu language syntax; JSON is not supported. With `-check` the command is read-only and acts as the formatting gate for CI.

## Verified example

```shell
tofu fmt -check -diff -recursive
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: exit status `0` with no output — all configuration files (root module, child module, test file) already matched the canonical format.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
