# force-unlock

[INTENT: REFERENCE]

Release a stuck lock on the current workspace.

## Usage

```shell
tofu force-unlock [options] LOCK_ID
```

## Options

- `-force` — do not ask for input for unlock confirmation.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`force-unlock` manually unlocks the state for the defined configuration. It removes the lock on the state for the current workspace and does not modify infrastructure. The lock behavior depends on the backend being used; local state files cannot be unlocked by another process. The mandatory `LOCK_ID` argument is the ID of the stuck lock, as reported by the failed operation that left it behind.

## Verified example

```shell
tofu force-unlock -force <LOCK_ID>
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox with a zero UUID: the command failed with `Failed to unlock state: LocalState not locked` — the verified error-path proof that no lock exists on the local state and that the command inspects real lock state instead of succeeding vacuously.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
