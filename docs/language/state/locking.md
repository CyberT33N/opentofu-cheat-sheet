# State locking

[INTENT: REFERENCE]

State locking prevents concurrent operations from corrupting the state: backends that support locking hold a lock during operations (`-lock`, `-lock-timeout`), and a stuck lock is released with [`tofu force-unlock`](../../cli/force-unlock/overview.md). The official language tree carries this topic as a page of the [state](overview.md) area.

## Official documentation

- [State Locking](https://opentofu.org/docs/language/state/locking/)
