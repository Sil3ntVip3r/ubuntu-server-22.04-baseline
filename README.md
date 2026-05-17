# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 provisioning, hardening, and tuning baseline for:

- VPS infrastructure
- Blockchain and masternode servers
- Docker hosts
- RPC nodes
- Build servers
- General Ubuntu 22.04 infrastructure

---

## Features

### Interactive Provisioning

The setup script interactively prompts for:

- Hostname
- Server role
- Provider/location
- Sudo admin username
- Swap sizing
- SSH key setup method
- Extra firewall ports
- Root password handling
- Optional reboot

---

## Swap Management

Supports:

- Auto-recommended swap sizing based on RAM and server role
- Custom swap sizing
- Persistent swap configuration
- Existing swap detection
- Safe swap rebuild logic

Examples:

```text
2G
8G
20G
32768M
```

### Auto Swap Recommendations

| Server Type / RAM | Recommended Swap |
|---|---|
| Small VPS (<=2GB RAM) | 4G |
| 4GB RAM | 4G |
| 8GB RAM | 8G |
| 16GB-32GB RAM | 16G |
| Blockchain / Docker / Build / RPC nodes | 20G |

---

## Security Features

### SSH Hardening

- Root SSH login disabled
- SSH password authentication disabled
- SSH key authentication enabled
- Configurable sudo admin user
- SSH session hardening
- SSH config validation before restart

### Firewall and Protection

- UFW firewall
- SSH port automatically opened
- Optional additional TCP/UDP ports
- Fail2Ban enabled

### Root Account Security

- Optional root password reset
- Optional root password locking
- Recovery-safe design

---

## System Tuning

### Sysctl Tuning

Includes:

- Reduced swap aggressiveness
- Filesystem cache tuning
- SSD write tuning
- BBR congestion control
- TCP backlog tuning
- Kernel panic auto reboot
- inotify scaling

### System Limits

Configures:

- nofile limits
- nproc limits
- PAM limits
- systemd limits

Defaults:

```text
500000
```

---

## Time Synchronization

Uses:

- Chrony
- UTC timezone
- North America and Ubuntu NTP pools

Removes conflicting:

- ntp
- systemd-timesyncd

---

## SSD/NVMe Optimization

Includes:

- fstrim timer
- SSD write tuning
- NVMe utilities
- SMART monitoring tools

---

## Installed Utility Packages

Includes:

- htop
- btop
- iotop
- iftop
- nvme-cli
- smartmontools
- jq
- tmux
- rsync
- fail2ban
- ufw
- chrony
- unattended-upgrades
- needrestart

---

## Logging and Backups

Each run creates:

```text
/root/system-setup-logs/YYYYMMDD-HHMMSS/
/root/system-setup-backups/YYYYMMDD-HHMMSS/
```

Includes:

- console logs
- configuration backups
- server summaries

---

## Verification Script

Automatically generates:

```text
/root/ubuntu22-verify.sh
```

Checks:

- swap
- sysctl
- firewall
- fail2ban
- chrony
- SSH settings
- limits
- installed packages
- summaries
- backups

---

## Repository Structure

```text
ubuntu-server-22.04-baseline/
├── CHANGELOG.md
├── README.md
├── docs/
│   └── recovery.md
├── setup/
│   └── ubuntu22-system-setup.sh
```

---

## Usage

Clone repository:

```bash
git clone https://github.com/Sil3ntVip3r/ubuntu-server-22.04-baseline.git
cd ubuntu-server-22.04-baseline
```

Run dry-run mode:

```bash
sudo bash setup/ubuntu22-system-setup.sh
```

Apply changes:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply
```

---

## Recommended Workflow

1. Run dry-run first
2. Run apply mode
3. Open a second terminal
4. Verify new SSH admin login works
5. Run verification script
6. Reboot server

---

## Verification

Run:

```bash
sudo bash /root/ubuntu22-verify.sh
```

---

## Versioning

Current baseline version:

```text
v1.1.0
```

---

## Recovery

See:

```text
docs/recovery.md
```
