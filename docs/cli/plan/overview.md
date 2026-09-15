# plan

[INTENT: REFERENCE]

Show changes required by the current configuration.

## Usage

```shell
tofu plan [options]
```

## Options

Plan customization options (also accepted by `tofu apply` when no saved plan is passed):

- `-destroy` — select the destroy planning mode: plan to destroy all currently managed objects.
- `-refresh-only` — select the refresh-only planning mode: check whether remote objects still match the most recent apply, without proposing actions to undo out-of-band changes.
- `-refresh=false` — skip checking for external changes to remote objects while creating the plan.
- `-replace=resource` — force replacement of a particular resource instance; repeatable.
- `-target=resource` — limit planning to the given module, resource, or instance and its dependencies; repeatable; cannot be used with `-exclude`.
- `-target-file=filename` — like `-target`, but reads resource addresses from a file.
- `-exclude=resource` — exclude the given object and everything depending on it; repeatable; cannot be used with `-target`.
- `-exclude-file=filename` — like `-exclude`, but reads resource addresses from a file.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.

Other options:

- `-detailed-exitcode` — return detailed exit codes: `0` = succeeded, no changes; `1` = planning failed; `2` = succeeded, changes proposed.
- `-out=path` — write a plan file that can be passed to `tofu apply`.
- `-generate-config-out=path` — (experimental) generate HCL for imported resources when import blocks are present.
- `-input=false` — disable prompting for unset required input variables.
- `-lock=false` / `-lock-timeout=duration` — state locking control.
- `-parallelism=n` — limit concurrent operations (default 10).
- `-state=statefile` — legacy option for the local backend only.
- `-show-sensitive` — do not redact sensitive values in the UI output.
- `-concise` — disable progress-related messages.
- `-compact-warnings`, `-consolidate-warnings=false`, `-consolidate-errors` — warning/error presentation control.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-deprecation=module:m` — control deprecation warnings (`all`, `local`, `none`; default `all`).
- `-no-color` — disable colored output.

## Architectural explanation

`plan` generates a speculative execution plan: it shows which actions OpenTofu would take to reach the state described by the configuration, without performing them. Saving the plan with `-out` freezes the decision; `tofu apply <planfile>` then executes exactly those actions without re-planning — the canonical separation between decision and execution in automation.

## Saved plan content and plan encryption

The saved plan file carries the full configuration, the values associated with the planned changes, and the plan options including the input variables — treat it as a potentially sensitive artifact. With plan encryption enabled (the `encryption` block's `plan` section), the file is the encrypted envelope: only the encryption metadata alias is readable and the payload is ciphertext. Verified in the state-home birth window: the saved plan of an encryption-carrying root opened with `{"meta":{"state-encryption":"..."}}` and carried no plaintext configuration.

## Verified example

```shell
tofu plan -out=tfplan -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the plan proposed `2 to add, 0 to change, 0 to destroy` (one `terraform_data` resource in the root module, one in the child module) and was saved to `tfplan`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
