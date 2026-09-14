# state replace-provider

[INTENT: REFERENCE]

Replace provider in the state.

## Usage

```shell
tofu state replace-provider [options] FROM_PROVIDER_FQN TO_PROVIDER_FQN
```

## Options

- `-auto-approve` — skip interactive approval.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-ignore-remote-version` — rare option for the remote backend only.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-state`, `-state-out`, `-backup` — legacy options supported for the local backend only.

## Architectural explanation

`state replace-provider` replaces the provider for resources in the OpenTofu state, rewriting every matching provider reference from `FROM_PROVIDER_FQN` to `TO_PROVIDER_FQN` (fully qualified provider names, for example `hashicorp/null` to `example.com/namespace/null`). This is the migration surface when a configuration moves between provider forks or registries without recreating the managed infrastructure.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
