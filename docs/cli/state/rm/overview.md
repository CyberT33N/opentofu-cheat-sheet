# state rm

[INTENT: REFERENCE]

Remove instances from the state.

## Usage

```shell
tofu state rm [options] ADDRESS...
```

Aliases: `state remove`.

## Options

- `-dry-run` — print what would have been removed without removing anything.
- `-backup=PATH` — path where OpenTofu should write the backup state.
- `-state=PATH` — path to the state file to update; defaults to the current workspace state.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-ignore-remote-version` — continue even if remote and local OpenTofu versions are incompatible (extreme caution; may result in an unusable workspace).
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`state rm` removes one or more items from the OpenTofu state, causing OpenTofu to "forget" those items without destroying them in the remote system. Giving the address of an entire module removes all instances in that module and its child modules; giving the address of a resource with `count` or `for_each` removes all of its instances. Available instances can be listed with [state list](../list/overview.md).

## Verified example

```shell
tofu state rm terraform_data.renamed
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox after [state mv](../mv/overview.md): `Removed terraform_data.renamed` — `Successfully removed 1 resource instance(s).`; a subsequent `state list` showed only `module.greeting.terraform_data.this`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
