# destroy

[INTENT: REFERENCE]

Destroy previously-created infrastructure.

## Usage

```shell
tofu destroy [options]
```

## Options

- `-suppress-forget-errors` — suppress the error that occurs when a destroy operation completes successfully but leaves forgotten instances behind.

This command also accepts many of the plan-customization options accepted by `tofu plan` (see [plan](../plan/overview.md)), including `-auto-approve`, `-target`, `-exclude`, `-var`, `-var-file`, `-lock`, `-lock-timeout`, `-parallelism`, `-no-color`, `-json`, and `-json-into`.

## Architectural explanation

`destroy` is a convenience alias for `tofu apply -destroy`: it plans the destruction of all objects currently managed by the configuration and, after approval (or `-auto-approve`), executes it. The command removes only what the state tracks — it never touches resources outside the configuration's management.

## Verified example

```shell
tofu destroy -auto-approve -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Destroy complete! Resources: 2 destroyed.` — both `terraform_data` instances (root module and child module) were destroyed.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
