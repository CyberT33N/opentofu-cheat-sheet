# logout

[INTENT: REFERENCE]

Remove locally-stored credentials for a remote host.

## Usage

```shell
tofu logout [hostname]
```

## Architectural explanation

`logout` removes locally-stored credentials for the specified hostname from the local credentials file (`%APPDATA%\terraform.d\credentials.tfrc.json` on Windows). The API token is only removed from local storage, not destroyed on the remote server — it remains valid until manually revoked there.

## Verified example

```shell
tofu logout nonexistent-host.example.com
```

Verified on OpenTofu v1.12.5 (windows_amd64): `No credentials for nonexistent-host.example.com are stored.` — the command inspects only the local credentials file and is a safe local no-op for hosts without stored credentials.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
