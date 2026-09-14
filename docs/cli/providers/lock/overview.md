# providers lock

[INTENT: REFERENCE]

Write out dependency locks for the configured providers.

## Usage

```shell
tofu providers lock [options] [providers...]
```

## Options

- `-fs-mirror=dir` — consult the given filesystem mirror directory instead of the origin registry for each of the given providers; valid checksums are then limited to what the mirror contains.
- `-net-mirror=url` — consult the given network mirror (base URL) instead of the origin registry.
- `-platform=os_arch` — choose a target platform to request package checksums for (for example `linux_amd64`); repeatable for multi-platform lock files.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

The dependency lock file (`.terraform.lock.hcl`) is normally updated automatically by `tofu init`, but the information available to the normal provider installer can be constrained when installing from filesystem or network mirrors, leaving the lock file incomplete. `providers lock` updates the lock file based on the official packages available in the origin registry, ignoring the configured installation strategy. After success, the lock file contains checksums that allow installing the providers on all selected platforms. Without provider arguments, every provider declared in the configuration is updated.

## Verified example

```shell
tofu providers lock -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Success! OpenTofu has validated the lock file and found no need for changes.` — with the finding `- Skipping terraform.io/builtin/terraform because it is built in to OpenTofu CLI`: built-in providers never enter the lock file.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
