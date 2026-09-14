# taint

[INTENT: REFERENCE]

Mark a resource instance as not fully functional.

## Usage

```shell
tofu taint [options] <address>
```

## Options

- `-allow-missing` — succeed (exit code 0) even if the resource is missing.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-ignore-remote-version` — rare option for the remote backend only.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-state`, `-state-out`, `-backup` — legacy options supported for the local backend only.

## Architectural explanation

A "tainted" resource instance is one that may not be fully functional — either because its creation partially failed or because it was manually marked with this command. `taint` does not modify infrastructure directly, but subsequent plans will include actions to destroy the remote object and create a new object to replace it. The address uses the usual resource address syntax (`aws_instance.foo`, `aws_instance.bar[1]`, `module.foo.aws_instance.baz`); use shell quoting so the address reaches OpenTofu without special interpretation. The mark is removed with [untaint](../untaint/overview.md).

## Verified example

```shell
tofu taint terraform_data.example
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Resource instance terraform_data.example has been marked as tainted.`

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
