# Language Conventions

Binding rules for `docs/language`, the OpenTofu language reference area. Parent conventions: [Documentation conventions](../CONVENTIONS.md).

## Structure mirror

- `docs/language` mirrors the official OpenTofu language documentation tree 1:1. The authoritative structure source is `website/docs/language` in the official `opentofu/opentofu` repository, rendered at [opentofu.org/docs/language](https://opentofu.org/docs/language/).
- An official documentation **directory** becomes a folder carrying an `overview.md` (the directory's `index.mdx` equivalent) plus one child entry per official page.
- An official standalone **page** becomes a single `.md` file named byte-exactly after the official page slug (for example `attr-as-blocks.md`, `depends_on.md`).
- Folder and file names equal the official slugs byte-exactly. They are tool-fixed identifiers and are never restyled.
- Site-navigation metadata (`_category_.json`) and embedded code-sample files (`*.tf`, `*.ps1` under `examples/` trees) are not documentation endpoints and are excluded from the mirror.

## Files

- Every folder carries an `overview.md` navigation index of its children.
- Leaf pages carry the topic definition sourced from the official documentation or from the programmatic surface of the locally installed CLI, plus the canonical official link.
- `functions/` carries one page per built-in function; the single source of truth for the function catalog is the programmatic surface `tofu metadata functions -json` of the locally installed version, cross-checked against the official function pages.

## Page layout (topic pages)

1. `# <topic name>` — the official topic name.
2. `[INTENT: REFERENCE]` marker.
3. Scope definition — what the topic covers, sourced from the official documentation or the programmatic surface.
4. `## Official documentation` — the canonical upstream link.

## Verification

- Language semantics are documented only from the official documentation or from the programmatic surface of the locally installed CLI (`tofu metadata functions -json`, `tofu console`, `tofu providers schema -json`).
- Completeness is binary: every official documentation page and every built-in function present in the programmatic catalog is documented; nothing else is documented.
