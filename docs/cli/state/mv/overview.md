# state mv

[INTENT: REFERENCE]

Move an item in the state.

## Usage

```shell
tofu state mv [options] SOURCE DESTINATION
```

Aliases: `state move`.

## Options

- `-dry-run` — print what would have been moved without moving anything.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-ignore-remote-version` — rare option for the remote backend only.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-state`, `-state-out`, `-backup` — legacy options supported for the local backend only.

## Architectural explanation

`state mv` moves the item matched by the source address to the destination address — also across state files. Use cases: resource renaming, moving items into or out of modules, moving entire modules, and refactoring one configuration into multiple separately managed configurations. Because the command is destructive in nature, it always writes a backup copy of the state before saving changes; the backup cannot be disabled. When moving to a different state file, a backup is created for each state file.

## Verified example

```shell
tofu state mv terraform_data.example terraform_data.renamed
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Move "terraform_data.example" to "terraform_data.renamed"` — `Successfully moved 1 object(s).`

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
