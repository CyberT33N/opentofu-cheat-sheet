# Output values

[INTENT: REFERENCE]

Output values are the results a module exports, declared with the `output` block and read from the state with [`tofu output`](../../../cli/output/overview.md). Root module outputs are printed after apply; child module outputs are referenced as `module.<NAME>.<OUTPUT>`. The official language tree carries this topic as a page of the [values](overview.md) area.

## Verified example

```hcl
output "greeting" {
  value = terraform_data.example.output
}
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: after apply, `tofu output` printed `greeting = "hello"` and `module_greeting = "hello"`.

## Official documentation

- [Output Values](https://opentofu.org/docs/language/values/outputs/)
