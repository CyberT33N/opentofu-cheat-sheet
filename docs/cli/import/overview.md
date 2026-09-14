# import

[INTENT: REFERENCE]

Associate existing infrastructure with a OpenTofu resource.

## Usage

```shell
tofu import [options] ADDR ID
```

## Options

- `-config=path` — path to a directory of configuration files used to configure the provider; defaults to the working directory.
- `-input=false` — disable interactive input prompts.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-ignore-remote-version` — rare option for the remote backend only.
- `-var 'foo=bar'` / `-var-file=foo` — set input variable values (only useful with `-config`).
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-compact-warnings`, `-consolidate-warnings`, `-consolidate-errors` — warning/error presentation control.
- `-no-color` — disable colored output.
- `-state`, `-state-out`, `-backup` — legacy options supported for the local backend only.

## Architectural explanation

`import` finds and imports an existing remote object into the OpenTofu state, bringing existing infrastructure under OpenTofu management without initially creating it through OpenTofu. `ADDR` is the target resource address in the configuration; `ID` is the resource-specific identifier the provider uses. The command does not modify infrastructure, but it makes network requests to inspect the imported object. For declarative, reviewable imports prefer the configuration-level `import` block (see [language/import](../../language/import/overview.md)).

## Verified example

```shell
tofu import terraform_data.example <RESOURCE_ID> -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Import successful!` — the built-in `terraform_data` resource accepts an arbitrary ID, was refreshed under that ID, and is from then on managed by OpenTofu.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
