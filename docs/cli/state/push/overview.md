# state push

[INTENT: REFERENCE]

Update remote state from a local state file.

## Usage

```shell
tofu state push [options] PATH
```

## Options

- `-force` — write the state even if lineages do not match or the remote serial is higher.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`state push` pushes a local state file and overwrites the remote state with it. The command protects against writing an older serial or a different state file lineage unless `-force` is specified. It also works with local state (overwriting the local state), but is less useful there. If `PATH` is `-`, the state is read from stdin; stdin data is not streamed to the backend but loaded completely (until pipe close), verified, and then pushed.

## Verified example

```shell
tofu state push terraform.tfstate
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the local state file was accepted and written back without error (matching lineage and serial — no `-force` required).

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
