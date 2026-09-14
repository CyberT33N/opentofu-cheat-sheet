# apply

[INTENT: REFERENCE]

Create or update infrastructure.

## Usage

```shell
tofu apply [options] [PLAN]
```

## Options

- `-auto-approve` — skip interactive approval of the plan before applying.
- `-backup=path` — path to back up the existing state file before modifying; defaults to the `-state-out` path with `.backup` extension; `-` disables the backup.
- `-destroy` — destroy OpenTofu-managed infrastructure (`tofu destroy` is a convenience alias for this option).
- `-input=true` — ask for input for variables if not directly set.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-parallelism=n` — limit parallel resource operations (default 10).
- `-state=path` / `-state-out=path` — state read/write paths for the local backend.
- `-show-sensitive` — display sensitive values.
- `-suppress-forget-errors` — suppress the error that occurs when a destroy completes but leaves forgotten instances behind.
- `-compact-warnings`, `-consolidate-warnings=false`, `-consolidate-errors` — warning/error presentation control.
- `-concise` — disable progress-related messages.
- `-var 'foo=bar'` / `-var-file=foo` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-deprecation=module:m` — control deprecation warnings (`all`, `local`, `none`).
- `-no-color` — disable colored output.

If no saved plan file is provided, `apply` also accepts all plan-customization options of `tofu plan` (see [plan](../plan/overview.md)).

## Architectural explanation

`apply` creates or updates infrastructure according to the configuration files in the current directory. Without a plan argument it generates a new plan and presents it for approval before taking any action; with a saved plan from `tofu plan -out=...` it executes exactly the described actions without any confirmation prompt — the deterministic path for CI/CD pipelines.

## Verified example

```shell
tofu apply -no-color tfplan
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox with the saved plan from [plan](../plan/overview.md): `Apply complete! Resources: 2 added, 0 changed, 0 destroyed.` with outputs `greeting = "hello"` and `module_greeting = "hello"`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
