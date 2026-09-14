# state pull

[INTENT: REFERENCE]

Pull current state and output to stdout.

## Usage

```shell
tofu state pull [options]
```

## Options

- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.

## Architectural explanation

`state pull` pulls the current state from its location, upgrades the local copy's state format to the current version, and outputs it to stdout. Its primary use is state stored remotely; with local state it still works but is less useful. Because the state is printed to stdout, the command is the canonical extraction surface for external state inspection tooling.

## Verified example

```shell
tofu state pull
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the complete state document was printed to stdout — `"version": 4`, `"terraform_version": "1.12.5"`, the state `serial`, the `lineage` UUID, the `outputs` map, and the `resources` array with both managed `terraform_data` instances.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
