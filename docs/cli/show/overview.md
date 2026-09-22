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
- `-module=DIR` — show the configuration of just a single module in the given directory, without requiring any dependencies to be installed (requires `-json`).

Other options:

- `-json` — show the information in machine-readable form.
- `-json-into=out.json` — the same output as `-json`, written directly to the given file.
- `-show-sensitive` — display sensitive values.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-no-color` — disable colored output.

## Architectural explanation

`show` reads and outputs an OpenTofu state or plan file in human-readable form. It is the inspection boundary for both artifacts of the plan/apply lifecycle: the saved plan (what will happen) and the state snapshot (what is managed). With `-json` the same content becomes the machine-readable input for external analysis tooling.

The configuration surfaces make the command the CLI's programmatic configuration-inspection boundary: `-config` returns the JSON configuration representation — exactly the configuration-related information the plan representation carries — without requiring a plan to be created first, and `-module=DIR` returns a subset of that representation for a single module directory without requiring `tofu init` or the module's dependencies. The `-module` subset deliberately omits the per-module-call `module` property, the resource `schema_version` property, and every expression-related property: it proves which resources, variables, and outputs a module declares, never their attribute values. The full configuration representation with expressions requires `-config` against an initialized working directory, because the provider plugins supply the schema knowledge.

## Verified example

```shell
tofu show -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the current state was rendered with both managed `terraform_data` instances and the `Outputs` section.

```shell
tofu show -module=. -json
```

Verified on OpenTofu v1.12.5 (windows_amd64) against a real module directory: exit 0 with the JSON configuration representation of the module — `provider_config` (name, full_name, version_constraint) plus `root_module` with its `outputs` (including their descriptions), `resources` (address, mode, type, name per declared resource), and `variables` (type, default, description, required per declared input) — and, as documented, without any expression-related properties.

## Troubleshooting: the PowerShell carrier form

On Windows PowerShell, an inline `-module=.` argument is mangled at the native-command boundary (the engine reports either a positional-argument error or the literal unexpanded variable name). The proven carrier form is the `cmd /c` subshell: `cmd /c "tofu show -module=. -json"`. Verified on OpenTofu v1.12.5 (windows_amd64): both mangled forms failed before any read; the `cmd /c` form returned the JSON document.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
