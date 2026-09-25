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

## Troubleshooting: variable resolution with a saved plan

With a saved plan file, no plan-customization options are accepted — `-var` and `-var-file` are rejected in that mode. A configuration whose `encryption` block references a variable still needs that variable resolved at apply time, because the engine must decrypt the saved plan. The failure is fail-closed before any mutation: `Failed to request input from user for variable var.<name>` and `Unable to compute static value` on the `encryption` block. The proven channel is the environment variable form, which the saved-plan mode accepts: `TF_VAR_<name>`. Verified in the state-home birth window: `tofu apply -no-color birth.tfplan` failed fail-closed without the variable, and `cmd /c "set TF_VAR_state_encryption_key=<KEY_RESOURCE> && tofu apply -no-color birth.tfplan"` applied exactly the saved plan (`Apply complete! Resources: 2 added, 0 changed, 0 destroyed.`).

## Troubleshooting: the cmd set carrier must not leak a trailing space

When the `TF_VAR_<name>` channel is bound through `cmd /c "set TF_VAR_<name>=<VALUE> && tofu apply ..."`, a space between the value and the `&&` separator becomes part of the variable value, because the `cmd` `set` builtin assigns everything up to the command separator. A resource-reference variable then fails fail-closed before any mutation with `Resource name [...] does not match any known resource name pattern`. The canonical safe carrier is the quoted assignment form, which binds the value exactly: `cmd /c 'set "TF_VAR_<name>=<VALUE>" && tofu apply -no-color <PLAN>'`. Verified in the control-zone state-home window: the unquoted form with a space before `&&` failed with the resource-name pattern error on the encryption key reference, and the quoted form applied exactly the saved plan (`Apply complete! Resources: 2 added, 0 changed, 0 destroyed.`).

## Verified example

```shell
tofu apply -no-color tfplan
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox with the saved plan from [plan](../plan/overview.md): `Apply complete! Resources: 2 added, 0 changed, 0 destroyed.` with outputs `greeting = "hello"` and `module_greeting = "hello"`.

## Troubleshooting: engine-driven Cloud Run job updates require `actAs` on the execution identity

Verified on OpenTofu v1.12.5 (windows_amd64) against a live Google Cloud zone with the pinned provider v7.44.0: an apply that updates a `google_cloud_run_v2_job` whose template carries `service_account` fails per job with `googleapi: Error 403: Permission 'iam.serviceaccounts.actAs' denied on service account <SERVICE_ACCOUNT>` when the caller lacks `iam.serviceaccounts.actAs` on that identity. The role content proof matters: `roles/iam.serviceAccountAdmin` does NOT carry `actAs` (proven over `gcloud iam roles describe`); the predefined carrier is `roles/iam.serviceAccountUser`. The proven window form is a service-account-scoped grant of `roles/iam.serviceAccountUser` to the operator on exactly the affected execution identities, with a read-back per grant and its removal at hardening.

## Troubleshooting: a saved plan is stale after a partial apply changed the state

Verified on OpenTofu v1.12.5 (windows_amd64): re-applying a saved plan after an earlier apply run already persisted part of its actions fails before any mutation with `Error: Saved plan is stale` ("The given plan file can no longer be applied because the state was changed by another operation after the plan was created."). The state change by the own earlier apply is enough — no external actor is required. The resolution form: regenerate the plan against the current state (`tofu plan -out=...`); the regenerated plan shows exactly the remaining actions (already-persisted imports, creates, and updates drop out), and that plan applies cleanly.

## Troubleshooting: IAM conditions on primitive roles are rejected at apply time

Verified on OpenTofu v1.12.5 (windows_amd64) against a live Google Cloud project with the pinned provider v7.44.0: a `google_project_iam_member` that combines a primitive role (`roles/owner`, `roles/editor`, `roles/viewer`) with a `condition` block fails at apply with `googleapi: Error 400: LintValidationUnits/BindingRoleAllowConditionCheck Error: Conditions can't be set on primitive roles., badRequest`. The failure is fail-closed before any mutation of the policy and isolated to that resource — independent resources of the same apply complete normally. The CLI reference states the same restriction on the `--condition` flag ("`--role` cannot be a basic role"). Time-bound or otherwise conditioned bindings require a non-primitive role (predefined or custom); a primitive role can only ever be bound unconditionally.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
