# Installation on Windows

[INTENT: REFERENCE]

Install OpenTofu from the winget repository:

```powershell
winget install --exact --id=OpenTofu.Tofu
```

Verify the installation:

```powershell
tofu -version
```

If winget-installed `tofu` does not resolve, make sure that `%LOCALAPPDATA%\Microsoft\WinGet\Links` is in your `PATH` environment variable.

Alternatively, OpenTofu is available on the scoop repository:

```powershell
scoop bucket add main
scoop install main/opentofu
```

## Verified installation evidence

The local machine runs OpenTofu installed through winget: `tofu.exe` resolves through `%LOCALAPPDATA%\Microsoft\WinGet\Links\tofu.exe`, and `tofu version` reports `OpenTofu v1.12.5 on windows_amd64`.

Official documentation: [Installing OpenTofu on Windows](https://opentofu.org/docs/intro/install/windows/)
