# graph

[INTENT: REFERENCE]

Generate a Graphviz graph of the steps in an operation.

## Usage

```shell
tofu graph [options]
```

## Options

- `-plan=tfplan` — render the graph using the specified plan file instead of the configuration in the current directory.
- `-draw-cycles` — highlight any cycles in the graph with colored edges (helps when diagnosing cycle errors).
- `-type=plan` — type of graph to output: `plan`, `plan-refresh-only`, `plan-destroy`, or `apply`. By default OpenTofu chooses `plan`, or `apply` if `-plan=...` is also set.
- `-module-depth=n` — (deprecated) in prior versions, specified the depth of modules to show.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.

## Architectural explanation

`graph` produces a representation of the dependency graph between the objects in the current configuration and state, emitted in the DOT language. Any GraphViz-compatible renderer (or compatible web service) can visualize it. The graph makes the implicit dependency order — resources, modules, variables, outputs, providers — inspectable, which is the primary diagnostic surface for ordering and cycle problems.

## Verified example

```shell
tofu graph -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: a `digraph` was emitted whose edges map the verified dependency order — for example `output.greeting` depends on `terraform_data.example`, and `module.greeting.terraform_data.this` depends on `provider["terraform.io/builtin/terraform"]`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
