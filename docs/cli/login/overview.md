# login

[INTENT: REFERENCE]

Obtain and save credentials for a remote host.

## Usage

```shell
tofu login [hostname]
```

## Architectural explanation

`login` retrieves an authentication token for the given hostname, if it supports automatic login, and saves it in a credentials file in the home directory. Unless overridden by credentials helper settings in the CLI configuration, the credentials are written to `%APPDATA%\terraform.d\credentials.tfrc.json` on Windows (`~/.terraform.d/credentials.tfrc.json` on Unix-like systems).

## Deferred verification

`login` is production-bound: it performs an interactive token flow against a real remote host and writes productive credentials. It is therefore documented from its verified help surface without a fabricated local example; the live verification is owed to an interactive session against the target host.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
