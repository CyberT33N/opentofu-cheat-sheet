# get

[INTENT: REFERENCE]

Install or upgrade remote OpenTofu modules.

## Usage

```shell
tofu get [options]
```

## Options

- `-update` — check already-downloaded modules for available updates and install the newest versions available.
- `-test-directory=path` — set the test directory, defaults to `tests`.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-no-color` — disable colored output.

## Architectural explanation

`get` downloads and installs the modules needed for the configuration in the current working directory, recursively resolving modules imported by modules. An already-downloaded module is not re-downloaded or checked for updates unless `-update` is given. Module installation also happens automatically as part of `tofu init`, so `get` is rarely needed separately — its standalone value is the explicit `-update` pass.

## Verified example

```shell
tofu get -update -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox with a local child module: `- greeting in modules/greeting` — the local module was resolved and registered.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
