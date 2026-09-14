# Installation on Ubuntu

[INTENT: REFERENCE]

## Snap

OpenTofu is available on Snapcraft (Snap is available by default on Ubuntu):

```bash
snap install --classic opentofu
```

## Debian repository (.deb)

Install OpenTofu from the official Debian repository using the installer script:

```bash
curl --proto '=https' --tlsv1.2 -fsSL https://get.opentofu.org/install-opentofu.sh -o install-opentofu.sh
chmod +x install-opentofu.sh
# Inspect the downloaded script before running it.
./install-opentofu.sh --install-method deb
rm -f install-opentofu.sh
```

Or set up the repository step by step:

```bash
# Install tooling:
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg

# Install the OpenTofu GPG keys:
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://get.opentofu.org/opentofu.gpg | sudo tee /etc/apt/keyrings/opentofu.gpg >/dev/null
curl -fsSL https://packages.opentofu.org/opentofu/tofu/gpgkey | sudo gpg --no-tty --batch --dearmor -o /etc/apt/keyrings/opentofu-repo.gpg >/dev/null
sudo chmod a+r /etc/apt/keyrings/opentofu.gpg /etc/apt/keyrings/opentofu-repo.gpg

# Create the OpenTofu source list:
echo \
  "deb [signed-by=/etc/apt/keyrings/opentofu.gpg,/etc/apt/keyrings/opentofu-repo.gpg] https://packages.opentofu.org/opentofu/tofu/any/ any main
deb-src [signed-by=/etc/apt/keyrings/opentofu.gpg,/etc/apt/keyrings/opentofu-repo.gpg] https://packages.opentofu.org/opentofu/tofu/any/ any main" | \
  sudo tee /etc/apt/sources.list.d/opentofu.list > /dev/null
sudo chmod a+r /etc/apt/sources.list.d/opentofu.list

# Install OpenTofu:
sudo apt-get update
sudo apt-get install -y tofu
```

Verify the installation:

```bash
tofu -version
```

Official documentation: [Installing OpenTofu via Snapcraft](https://opentofu.org/docs/intro/install/snap/) · [Installing OpenTofu on .deb-based Linux](https://opentofu.org/docs/intro/install/deb/)
