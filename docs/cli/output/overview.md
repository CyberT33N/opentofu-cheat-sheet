# output

[INTENT: REFERENCE]

Show output values from your root module.

## Usage

```shell
tofu output [options] [NAME]
```

## Options

- `-state=path` — path to the state file to read; defaults to `terraform.tfstate`; ignored when remote state is used.
- `-json` — machine-readable output in JSON format.
- `-json-into=out.json` — the same output as `-json`, written directly to the given file.
- `-raw` — for value types convertible to string, print the raw string directly instead of a human-oriented representation (use with care when stdout is a terminal and the value might contain control characters).
- `-show-sensitive` — display sensitive values.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-no-color` — disable colored output.

## Architectural explanation

`output` reads output values from the OpenTofu state and prints them. Without `NAME` all outputs of the root module are printed; with `NAME` only the named one. `-raw` and `-json` are the scripting surfaces: `-raw` for shell substitution, `-json` for structured consumers (including the `sensitive` marker per output).

## Verified example

```shell
tofu output -no-color
tofu output -json
tofu output -raw greeting
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox after [apply](../apply/overview.md): plain output printed both outputs, `-json` printed them with `sensitive: false` and type metadata, and `-raw greeting` printed `hello` without a trailing newline.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
