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

## Troubleshooting: validation cross-references must never form a cycle

A plan that fails with `Error: Cycle` listing variable expansions and a local (for example `var.<a> (expand, reference), var.<b> (expand, reference), local.<x> (expand)`) reports a dependency cycle in the evaluation graph, not a formatting or value problem. The proven trigger: two `validation` blocks that reference each other's variable — directly or through a local — so the evaluation of each condition depends on the other. The resolution is the unidirectional form: bind the consistency check against the static declared topology of the configuration (for example a static local) instead of a second variable, so the reference graph stays acyclic. Verified on OpenTofu v1.12.5 (windows_amd64): the bidirectional pair failed every plan with `Error: Cycle` before any evaluation; the unidirectional form evaluated fail-closed on a violating value and passed on a valid one.

## Troubleshooting: org-policy reads fail with `403 SERVICE_DISABLED` under ADC (quota project)

A plan or apply that touches `google_org_policy_policy` (or any other API that requires a quota project under ADC) fails with `googleapi: Error 403 ... The orgpolicy.googleapis.com API requires a quota project` attributed to the gcloud default consumer project when the engine runs under user ADC without the provider-side quota binding. Binding the quota project into the ADC file via `gcloud auth application-default set-quota-project <PROJECT_ID>` is necessary but not sufficient: the pinned Google provider sends the `X-Goog-User-Project` header only when `user_project_override = true` and a billing project are both set. The proven carrier form binds both on the engine process (provider v7.44.0):

```powershell
cmd /c 'set "USER_PROJECT_OVERRIDE=true" && set "GOOGLE_BILLING_PROJECT=<PROJECT_ID>" && set "GOOGLE_CLOUD_QUOTA_PROJECT=<PROJECT_ID>" && tofu plan -input=false -no-color -var-file=window.tfvars'
```

The caller needs `serviceusage.services.use` on the quota project (for example via `roles/serviceusage.serviceUsageConsumer`), and the API must be enabled on the quota project. Verified on OpenTofu v1.12.5 (windows_amd64) against the pinned provider v7.44.0: the plan failed twice without the pair (ADC file only, then a misnamed env binding) and completed with exit 2 once `USER_PROJECT_OVERRIDE` plus the billing project were bound on the process.

## Troubleshooting: IAM bindings survive `plan` — proven read-only against the environment (OpenTofu v1.12.x)

Verified on OpenTofu v1.12.5 (windows_amd64) against a live Google Cloud zone with the pinned provider v7.44.0: with 16 operator IAM bindings freshly granted and read-back-proven on the zone projects and the organization, `tofu plan -input=false -no-color -var-file=window.tfvars -out=window.tfplan` completed with exit 0 and proposed zero destroy actions, and the full IAM read-back immediately after the run proved every binding intact. The project's admin activity audit log (`logName:"cloudaudit.googleapis.com" AND protoPayload.methodName:"SetIamPolicy"`) shows zero IAM writes between the grant and the post-plan read-back. The only write effect of `plan` is the local plan file under `-out` — matching the official contract: "The `plan` command alone does not actually carry out the proposed changes."

Incident-class resolution: when operator bindings are found missing after a window, the actor evidence lives in the admin activity audit log, never in the engine. A removal that fails with `Policy binding with the specified principal, role, and condition not found!` signals that the binding is already absent — the audit timeline then shows which earlier `SetIamPolicy` call removed it and under which identity.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
