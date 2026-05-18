# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 provisioning, hardening, tuning, verification, reusable configuration, update-management, and optional WireGuard VPN baseline for:

- VPS infrastructure
- Blockchain and masternode servers
- Docker hosts
- RPC nodes
- Build servers
- General Ubuntu 22.04 infrastructure

Designed for repeatable fleet provisioning with convergent/idempotent configuration handling.

Current baseline version:

```text
v1.6.0
```

---

# Features

## Interactive Provisioning

The setup script interactively prompts for:

- Hostname
- Server role
- Provider/location
- Sudo admin username
- Swap sizing mode
- System limits profile
- SSH key setup method
- Local admin password selection
- Root password handling
- Ubuntu update policy
- Unattended security updates
- Optional WireGuard VPN support
- Extra firewall ports
- Optional reboot

---

# WireGuard VPN Support

Optional WireGuard VPN support is now integrated directly into the baseline.

Reference:

urlWireGuard Official Sitehttps://www.wireguard.com/install/

## Supported Modes

### Install Only

Installs:

- wireguard
- wireguard-tools
- qrencode

without creating VPN configuration.

### Simple Server Mode

Automatically:

- generates WireGuard keys
- creates server config
- configures UFW UDP port
- enables wg-quick service
- creates VPN interface
- stores configs securely

## WireGuard Security Design

The baseline intentionally:

- never stores WireGuard private keys in reusable config files
- generates keys locally on the server
- stores configs with restrictive permissions
- avoids logging private key material

## Default WireGuard Settings

| Setting | Default |
|---|---|
| Interface | wg0 |
| UDP Port | 51820 |
| VPN Address | 10.100.0.1/24 |

## Future Fleet Benefits

WireGuard support enables:

- private inter-server networking
- private RPC infrastructure
- VPN-only SSH access
- hidden backend services
- encrypted management traffic
- future mesh networking

## WireGuard Files

```text
/etc/wireguard/
```

Generated files:

```text
wg0.conf
wg0.key
wg0.pub
```

---

# Ubuntu 22.04 Update Management

The baseline includes safe Ubuntu 22.04 patch management.

## What It Does

- installs Ubuntu 22.04 security updates
- installs Ubuntu 22.04 package updates
- installs kernel/security patches
- runs package cleanup automatically
- configures unattended security updates
- blocks Ubuntu release upgrades

## What It Prevents

The baseline prevents accidental:

- Ubuntu 22.04 -> 24.04 upgrades
- release-upgrade prompts
- unattended distro migrations

## Release Upgrade Policy

The script enforces:

```text
Prompt=never
```

inside:

```text
/etc/update-manager/release-upgrades
```

---

# Saved Configuration Workflow

Dry-run mode automatically saves reusable configuration files.

Configuration directory:

```text
/root/system-setup-configs/
```

Supports:

- reusable provisioning configs
- repeatable deployments
- apply-mode config reuse
- explicit config loading
- fleet consistency
- multi-server provisioning

---

# Security Features

## SSH Hardening

- Root SSH login disabled
- SSH password authentication disabled
- SSH key authentication enabled
- Configurable sudo admin user
- Public key paste, root key copy, or generated keypair options
- SSH config validation before restart
- Reduced SSH authentication attempts
- SSH keepalive tuning

## Firewall and Protection

- UFW firewall
- SSH port 22 automatically opened before firewall enablement
- Optional additional TCP/UDP ports
- Fail2Ban enabled
- Optional WireGuard UDP port support

## CPU Microcode Safety

The baseline now safely handles microcode installation.

### Current Behavior

- installs the correct vendor microcode package
- DOES NOT automatically remove opposite-vendor microcode packages
- prevents accidental kernel meta-package removal

### Example

Intel CPU:

- installs `intel-microcode`
- warns if `amd64-microcode` exists

AMD CPU:

- installs `amd64-microcode`
- warns if `intel-microcode` exists

### Why

Removing the opposite package can sometimes remove:

- linux-generic
- linux-image-generic
- kernel meta-packages

The safer approach is:

- install correct package automatically
- manually review removals later

---

# System Tuning

## Sysctl Tuning

Includes:

- Reduced swap aggressiveness
- Filesystem cache tuning
- SSD write tuning
- BBR congestion control
- TCP backlog tuning
- Kernel panic auto reboot
- inotify scaling

## Limits Integration

The selected limits profile is applied through:

- `/etc/security/limits.d/99-custom-limits.conf`
- PAM session limits
- systemd manager limits
- `fs.file-max` sysctl

---

# Logging, Backups, and Configs

Each run creates:

```text
/root/system-setup-logs/YYYYMMDD-HHMMSS/
/root/system-setup-backups/YYYYMMDD-HHMMSS/
/root/system-setup-configs/YYYYMMDD-HHMMSS.conf
```

Includes:

- full console log
- configuration backups
- reusable provisioning config
- server summary
- verification references

Summary file:

```text
/root/server-baseline-summary.txt
```

---

# Verification Script

Automatically generates:

```text
/root/ubuntu22-verify.sh
```

The verification script validates:

- Ubuntu release version
- release-upgrade policy
- unattended-upgrades
- reboot-required status
- swap
- sysctl values
- firewall
- fail2ban
- chrony
- SSH settings
- PAM limits
- systemd limits
- WireGuard installation
- WireGuard interfaces
- installed packages
- microcode packages
- saved configs
- summaries
- backups
- logs

## Run Verification

```bash
bash /root/ubuntu22-verify.sh
```

---

# Usage

Clone repository:

```bash
git clone https://github.com/Sil3ntVip3r/ubuntu-server-22.04-baseline.git
cd ubuntu-server-22.04-baseline
```

## Run Dry-Run Mode

```bash
sudo bash setup/ubuntu22-system-setup.sh
```

## Run Apply Mode

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply
```

## Run Apply Mode With Explicit Config

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply --config /root/system-setup-configs/example.conf
```

---

# Recommended Workflow

1. Run dry-run first
2. Save and review generated config
3. Reuse or edit config if needed
4. Run apply mode
5. Complete password prompts during apply mode
6. Open a second terminal
7. Verify the new sudo admin SSH login works
8. Run the generated verification script
9. Verify WireGuard if enabled
10. Reboot server if updates/kernel changes require it
11. Rerun verification after reboot

---

# Documentation

Recovery guide:

```text
docs/recovery.md
```

WireGuard guide:

```text
docs/wireguard.md
```
