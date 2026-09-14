# test

[INTENT: REFERENCE]

Execute integration tests for OpenTofu modules.

## Usage

```shell
tofu test [options]
```

## Options

- `-filter=testfile` — execute only the specified test files; repeatable; paths are relative to the current working directory even if `-test-directory` is set.
- `-test-directory=path` — set the test directory, defaults to `tests`; test files are searched in the current directory and in the one specified by the flag.
- `-verbose` — print the plan or state for each test run block as it executes.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-compact-warnings`, `-consolidate-warnings`, `-consolidate-errors` — warning/error presentation control.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-no-color` — disable colored output.

## Architectural explanation

`test` executes automated integration tests against the current configuration: OpenTofu searches for `.tftest.hcl` files in the configuration and testing directories, executes the testing `run` blocks in order, and verifies conditional checks and assertions against the created infrastructure. The command creates real infrastructure and attempts to clean it up on completion — monitor the output to ensure cleanup succeeded.

## Verified example

```shell
tofu test -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox with `tests/resource.tftest.hcl` containing a `run` block (`command = apply`) and an `assert` on the `terraform_data.example` output: `tests\resource.tftest.hcl... pass` — `Success! 1 passed, 0 failed.`

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
