# show

[INTENT: REFERENCE]

Show the current state or a saved plan.

## Usage

```shell
tofu show [target-selection-option] [other-options]
```

## Options

Target selection options (default: `-state`):

- `-state` — the latest state snapshot, if any.
- `-plan=FILENAME` — the plan from a saved plan file.
- `-config` — show the current configuration (requires `-json`).

Other options:

- `-json` — show the information in machine-readable form.
- `-json-into=out.json` — the same output as `-json`, written directly to the given file.
- `-show-sensitive` — display sensitive values.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-no-color` — disable colored output.

## Architectural explanation

`show` reads and outputs an OpenTofu state or plan file in human-readable form. It is the inspection boundary for both artifacts of the plan/apply lifecycle: the saved plan (what will happen) and the state snapshot (what is managed). With `-json` the same content becomes the machine-readable input for external analysis tooling.

## Verified example

```shell
tofu show -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the current state was rendered with both managed `terraform_data` instances and the `Outputs` section.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
