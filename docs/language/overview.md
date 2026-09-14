# OpenTofu Language

[INTENT: NAVIGATION]

Complete reference area for the OpenTofu configuration language, mirroring the [official OpenTofu language documentation](https://opentofu.org/docs/language/) tree 1:1 (authoritative structure source: `website/docs/language` in the official `opentofu/opentofu` repository).

The main purpose of the OpenTofu language is declaring resources, which represent infrastructure objects. All other language features exist only to make the definition of resources more flexible and convenient. The language is declarative: it describes an intended goal rather than the steps to reach that goal, and its syntax consists of blocks (containers with a type, labels, and a body), arguments (assigning a value to a name), and expressions (representing values).

## Areas

- [checks](checks/overview.md) — the `check` block: standalone validation rules inside a configuration
- [data-sources](data-sources/overview.md) — the `data` block: reading data published outside the current configuration
- [ephemerality](ephemerality/overview.md) — ephemeral resources and write-only attributes: values that never persist to state
- [expressions](expressions/overview.md) — expressions: the value language of arguments, conditions, and templates
- [files](files/overview.md) — the files of a configuration: `.tf`/`.tf.json`, override files, and the dependency lock file
- [functions](functions/overview.md) — the complete catalog of all 121 built-in functions, plus provider-defined functions
- [import](import/overview.md) — the `import` block: declaratively bringing existing infrastructure under management
- [linting](linting/overview.md) — linting and static analysis of configurations
- [meta-arguments](meta-arguments/overview.md) — `count`, `for_each`, `depends_on`, `lifecycle`, `enabled`, and provider selection
- [modules](modules/overview.md) — modules: packaging and reusing configurations (syntax, sources, development)
- [providers](providers/overview.md) — providers: the plugins that interact with cloud platforms and other APIs
- [resources](resources/overview.md) — the `resource` block: declaring infrastructure objects (syntax, behavior, provisioners)
- [settings](settings/overview.md) — the `terraform` settings block and backend configuration
- [state](state/overview.md) — state: purpose, storage, locking, encryption, remote access, workspaces
- [symbol-libraries](symbol-libraries/overview.md) — symbol libraries for tooling integrations
- [syntax](syntax/overview.md) — the native syntax, JSON syntax, and the style guide
- [values](values/overview.md) — input variables, output values, and local values

## Standalone pages

- [Attributes as blocks](attr-as-blocks.md) — the legacy attributes-as-blocks syntax mode
- [V1 compatibility promises](v1-compatibility-promises.md) — the compatibility promises of the OpenTofu v1 series
