# CLI Conventions

Binding rules for `docs/cli`, the `tofu` command reference area. Parent conventions: [Documentation conventions](../CONVENTIONS.md).

## Structure mirror

- `docs/cli` mirrors the official `tofu` CLI command hierarchy 1:1: one folder per command or command group, nested down to the last subcommand.
- Folder names equal the official command tokens exactly (for example `state`, `mv`, `force-unlock`). They are tool-fixed identifiers and are never restyled, translated, or renamed.
- The mirror covers the complete stable command surface of the locally installed OpenTofu version, as reported by `tofu -help` and the nested `tofu <path> -help` surfaces.

## Files

- Every folder that has documented content carries an `overview.md`.
- Every folder without documented content carries an empty `.git-keep` placeholder. Once content is added, the `.git-keep` is removed.
- `overview.md` on a command-group level (`state`, `workspace`, `providers`, `metadata`) is a navigation index of its children; on a command (leaf) level it documents the command.

## Command page layout

1. `# <command path>` — the command path without the `tofu` prefix (for example `# state list`).
2. One-sentence purpose.
3. `## Usage` — the verified boilerplate with semantic placeholders (`<RESOURCE_ID>`, `<ADDRESS>`, …).
4. `## Options` — the verified flag surface from the local help output.
5. `## Architectural explanation` — what the command does, why, and what the relevant flags and output fields mean.
6. `## Verified example` — a real executed invocation with its proven result.
7. Optional deep-dive sections for non-obvious behavior, failure modes, and troubleshooting findings.

## Verification

- A command is documented only after it has been executed and its result verified against the live system (100% functional proof). Commands that require production-bound or interactive remote flows (for example `login`) carry a deferred-verification note instead of a fabricated example.
- The command grammar is verified against the local `tofu <path> -help` surface and the [official OpenTofu CLI documentation](https://opentofu.org/docs/cli/).
- Findings from failures or misbehavior during verification are recorded in the page (troubleshooting capture).
