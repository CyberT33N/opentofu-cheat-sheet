# console

[INTENT: REFERENCE]

Try OpenTofu expressions at an interactive command prompt.

## Usage

```shell
tofu console [options]
```

## Options

- `-state=path` — legacy option for the local backend only.
- `-var 'foo=bar'` / `-var-file=foo` — set input variable values.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-compact-warnings`, `-consolidate-warnings`, `-consolidate-errors` — warning/error presentation control.
- `-json-into=out.json` — stream the output of the console to the given file.

## Architectural explanation

`console` starts an interactive console for experimenting with OpenTofu expressions. It loads the current state, so expressions can be explored and tested against real values before being used in configurations. The command never modifies state. When standard input is not a terminal (piped input), the console evaluates the piped expression and exits — the canonical way to probe [built-in functions](../../language/functions/overview.md) non-interactively.

## Verified example

```shell
echo 'max(1,2)' | tofu console
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the piped expression was evaluated and the console printed `2`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
