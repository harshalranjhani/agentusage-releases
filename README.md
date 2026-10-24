# agentusage collector

Prebuilt releases of `agentusage`, the collector CLI for a self-hosted Agent Usage dashboard. This repository hosts release assets only.

## Install or upgrade

Linux x86_64, Linux ARM64 and macOS on Apple silicon:

```sh
curl -fsSL https://github.com/harshalranjhani/agentusage-releases/releases/latest/download/install.sh | sh
agentusage version
```

The installer verifies the archive against `SHA256SUMS` and installs `~/.local/bin/agentusage` without sudo. Run it as the ordinary user whose AI client history you want to collect.

- `AGENTUSAGE_INSTALL_DIR=/path` installs elsewhere. The installer prints the `PATH` line to add when needed.
- `AGENTUSAGE_VERSION=0.1.0` pins a release. You can also use that release's own installer, `releases/download/v0.1.0/install.sh`.

To upgrade, run the installer again, then restart each installed collector service. `agentusage daemon status` shows its ID:

```sh
systemctl --user restart SERVICE_ID.service          # Linux
launchctl kickstart -k "gui/$(id -u)/SERVICE_ID"     # macOS
```

## Manual install

Download your platform's `agentusage_<os>_<arch>.tar.gz` and `SHA256SUMS` from a release, then:

```sh
sha256sum --check --ignore-missing SHA256SUMS     # macOS: shasum -a 256 --check --ignore-missing SHA256SUMS
tar -xzf agentusage_linux_amd64.tar.gz
mkdir -p ~/.local/bin && mv agentusage ~/.local/bin/
```

The binaries are unsigned. A copy downloaded in a macOS browser needs `xattr -d com.apple.quarantine agentusage` before it runs; `curl` downloads do not.

Windows and Intel Macs are not supported.
