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

`test` executes automated integration tests against the current configuration: OpenTofu searches for `.tftest.hcl`, `.tftest.json`, `.tofutest.hcl` and `.tofutest.json` files in the configuration and testing directories, executes the testing `run` blocks in order, and verifies conditional checks and assertions against the created infrastructure. When both a `.tftest.hcl` and a `.tofutest.hcl` file with the same base name exist, the `.tofutest.hcl` file takes precedence and the `.tftest.hcl` file is ignored. The command creates real infrastructure and attempts to clean it up on completion — monitor the output to ensure cleanup succeeded.

## Plan-mode runs and custom-condition proofs

A `run` block with `command = plan` executes a plan instead of an apply and creates no infrastructure; `plan_options { refresh = false }` additionally disables the remote refresh, so the run is fully offline apart from provider configuration. This is the canonical proof form for custom conditions: rejection paths are proven through `expect_failures = [var.<name>]` (a surface that exists exclusively for custom conditions written in the configuration — never for provider-internal validation errors), and acceptance paths through `assert` blocks referencing the configuration's resources, variables, outputs or modules. Variables referenced by module sources, backend configuration or the `encryption` block must be assigned when running the test surface (for example through `-var-file`); a `variables` block at file or run level overrides the file channel for the configuration evaluation.

Verified in the state-home birth window (OpenTofu v1.12.5, windows_amd64): `tofu test -no-color -var-file=window.tfvars` executed a `variables.tofutest.hcl` suite of one acceptance run plus twelve rejection runs against an encryption-carrying root — `Success! 13 passed, 0 failed.`, with no infrastructure created. The suite proved every custom condition of the root with concrete values, including a rejection run that surfaced a latent condition defect the static gates (format, initialization, validation) could never see.

## Verified example

```shell
tofu test -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox with `tests/resource.tftest.hcl` containing a `run` block (`command = apply`) and an `assert` on the `terraform_data.example` output: `tests\resource.tftest.hcl... pass` — `Success! 1 passed, 0 failed.`

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
