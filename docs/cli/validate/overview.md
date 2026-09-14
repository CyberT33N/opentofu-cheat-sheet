# validate

[INTENT: REFERENCE]

Check whether the configuration is valid.

## Usage

```shell
tofu validate [options]
```

## Options

- `-no-tests` — do not validate test files.
- `-compact-warnings`, `-consolidate-warnings`, `-consolidate-errors` — warning/error presentation control.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-test-directory=path` — set the test directory, defaults to `tests`.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-no-color` — disable colored output.

## Architectural explanation

`validate` checks whether a configuration is syntactically valid and internally consistent, referring only to the configuration itself — it never accesses remote services such as remote state or provider APIs. It is therefore safe to run automatically (post-save editor checks, CI steps for reusable modules). Validation requires an initialized working directory; use `tofu init -backend=false` to initialize for validation without touching a configured remote backend. To verify a configuration in the context of a particular run (workspace, variable values), use `tofu plan`, which includes an implied validation check.

## Verified example

```shell
tofu validate -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the initialized local sandbox: `Success! The configuration is valid.`

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
