# Acton RPM Tip Repository

This repository publishes tip Acton RPM packages built from the latest `main`
branch CI run. Use it for testing the newest Acton build before the next stable
release.

## Install

Import the Acton package signing key, add the tip repository, and install
Acton:

```sh
sudo rpm --import https://rpmtip.acton.now/acton.gpg
sudo tee /etc/yum.repos.d/acton-tip.repo >/dev/null <<'REPO'
[acton-tip]
name=Acton tip
baseurl=https://rpmtip.acton.now/$basearch
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://rpmtip.acton.now/acton.gpg
REPO
sudo dnf install -y acton
acton version
```

On systems that use `yum` instead of `dnf`, use the same repo file and run:

```sh
sudo yum install -y acton
```

## Upgrade

```sh
sudo dnf upgrade -y acton
```

## Remove

```sh
sudo dnf remove -y acton
sudo rm -f /etc/yum.repos.d/acton-tip.repo
```

## Repository Layout

DNF substitutes `$basearch` automatically. The published architecture
repositories are:

- `https://rpmtip.acton.now/x86_64`
- `https://rpmtip.acton.now/aarch64`

## Signing

Keep both signature checks enabled:

```ini
gpgcheck=1
repo_gpgcheck=1
```

The public key is published at `https://rpmtip.acton.now/acton.gpg`. The RPM
packages and the repository metadata are signed with the matching private key.
