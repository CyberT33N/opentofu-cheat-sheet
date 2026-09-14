# untaint

[INTENT: REFERENCE]

Remove the 'tainted' state from a resource instance.

## Usage

```shell
tofu untaint [options] name
```

## Options

- `-allow-missing` — succeed (exit code 0) even if the resource is missing.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-ignore-remote-version` — rare option for the remote backend only.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-state`, `-state-out`, `-backup` — legacy options supported for the local backend only.

## Architectural explanation

`untaint` removes the "tainted" mark (see [taint](../taint/overview.md)) from a resource instance, causing OpenTofu to see it as fully functional and not in need of replacement. It does not modify infrastructure directly; it only avoids OpenTofu planning to replace the instance in a future operation.

## Verified example

```shell
tofu untaint terraform_data.example
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox after [taint](../taint/overview.md): `Resource instance terraform_data.example has been successfully untainted.`

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
