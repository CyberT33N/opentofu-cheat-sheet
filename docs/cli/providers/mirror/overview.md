# providers mirror

[INTENT: REFERENCE]

Save local copies of all required provider plugins.

## Usage

```shell
tofu providers mirror [options] <target-dir>
```

## Options

- `-platform=os_arch` — choose which target platform to build the mirror for (for example `linux_amd64`); repeatable for multi-platform mirrors. By default packages for the current platform are obtained.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`providers mirror` populates a local directory with copies of the provider plugins needed for the current configuration, so the directory can serve as a filesystem mirror or as the basis for a network mirror — obtaining providers without access to their origin registries in the future. The mirror directory contains JSON index files that can be published with the mirrored packages on a static HTTP file server to produce a network mirror; those index files are ignored when the directory is used as a local filesystem mirror.

## Verified example

```shell
tofu providers mirror mirror-dir
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: with only the built-in provider required, the mirror completed with `- Skipping terraform.io/builtin/terraform because it is built in to OpenTofu CLI` — built-in providers are never mirrored.

## Troubleshooting

- The target directory must exist before the command runs. With a non-existing `<target-dir>` the command fails with `Failed to update indexes ... cannot search <target-dir>: The system cannot find the file specified.` Create the directory first, then rerun.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
