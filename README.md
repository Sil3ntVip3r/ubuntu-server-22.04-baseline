# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 provisioning, hardening, tuning, and verification baseline for:

- VPS infrastructure
- Blockchain and masternode servers
- Docker hosts
- RPC nodes
- Build servers
- General Ubuntu 22.04 infrastructure

Designed for repeatable fleet provisioning with convergent/idempotent configuration handling.

Current baseline version:

```text
v1.3.1
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
- Extra firewall ports
- Optional reboot

---

# Dry-Run vs Apply Mode

## Dry-Run Mode

Run:

```bash
sudo bash setup/ubuntu22-system-setup.sh
```

Dry-run mode:

- shows planned actions
- validates logic
- validates configuration choices
- previews changes
- does NOT modify the system
- does NOT restart services
- does NOT create users
- does NOT write configs
- does NOT prompt for hidden password entry

Password prompts are intentionally skipped during dry-run mode.

Example:

```text
DRY-RUN: Would securely prompt to set/change password during --apply mode.
```

This is expected behavior and not an error.

## Apply Mode

Run:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply
```

Apply mode:

- performs system changes
- writes configurations
- configures users
- installs/removes packages
- restarts services when needed
- securely prompts for passwords using Linux passwd

Passwords are:

- never logged
- never echoed
- never stored in variables
- never written to disk by the script

---

# Swap Management

Supports:

- Auto-recommended swap sizing based on RAM and server role
- Custom swap sizing
- Persistent swap configuration
- Existing swap detection
- Safe swap rebuild logic
- Idempotent swap handling

Examples:

```text
2G
8G
20G
32768M
```

## Auto Swap Recommendations

| Server Type / RAM | Recommended Swap |
|---|---:|
| Small VPS <=2GB RAM | 4G |
| 4GB RAM | 4G |
| 8GB RAM | 8G |
| 16GB-32GB RAM | 16G |
| Blockchain / Docker / Build / RPC nodes | 20G |

---

# System Limits Profiles

The script supports selectable limits profiles:

| Profile | nofile / open files | nproc / processes | fs.file-max |
|---|---:|---:|---:|
| Conservative | 65,535 | 65,535 | 1,048,576 |
| Recommended | 500,000 | 500,000 | 2,097,152 |
| Max | 1,048,576 | 1,048,576 | 4,194,304 |
| Custom | User-defined | User-defined | User-defined |

## Recommended Default

For most VPS, blockchain, Docker, and RPC servers:

```text
Recommended
```

---

# Security Features

## SSH Hardening

- Root SSH login disabled
- SSH password authentication disabled
- SSH key authentication enabled
- Configurable sudo admin user
- Public key paste, root key copy, or generated keypair options
- SSH session hardening
- SSH config validation before restart
- Reduced SSH authentication attempts
- SSH keepalive tuning

## Local Password Handling

The script can:

- set a local admin password
- set/change the root password
- optionally lock the root password

Local passwords remain useful for:

- console access
- VPS web consoles
- recovery mode
- sudo prompts
- maintenance operations

## Firewall and Protection

- UFW firewall
- SSH port 22 automatically opened before firewall enablement
- Optional additional TCP/UDP ports
- Fail2Ban enabled

## Recommended Security Defaults

Recommended production setup:

- Disable root SSH login
- Disable SSH password authentication
- Use SSH keys only
- Set a known local admin password
- Set a known local root password
- Do not lock the root password unless alternate recovery access exists

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

# CPU Microcode Handling

The script automatically installs the correct CPU microcode package and removes the incorrect vendor package.

## Intel CPUs

- installs `intel-microcode`
- removes `amd64-microcode`

## AMD CPUs

- installs `amd64-microcode`
- removes `intel-microcode`

This improves:

- fleet consistency
- package cleanliness
- update consistency
- verification accuracy

---

# Time Synchronization

Uses:

- Chrony
- UTC timezone
- North America and Ubuntu NTP pools

Conflicting services removed/disabled:

- legacy `ntp`
- `systemd-timesyncd`

---

# SSD/NVMe Optimization

Includes:

- fstrim timer
- SSD write tuning
- NVMe utilities
- SMART monitoring tools

---

# Installed Utility Packages

Includes:

- htop
- btop
- iotop
- iftop
- nvme-cli
- smartmontools
- curl
- wget
- unzip
- jq
- git
- net-tools
- dnsutils
- tmux
- rsync
- lsof
- fail2ban
- ufw
- chrony
- unattended-upgrades
- needrestart
- logrotate
- sudo
- openssh-server

---

# Logging and Backups

Each run creates:

```text
/root/system-setup-logs/YYYYMMDD-HHMMSS/
/root/system-setup-backups/YYYYMMDD-HHMMSS/
```

Includes:

- full console log
- configuration backups
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

The verification script is safe to rerun any time.

It validates:

- swap
- sysctl values
- firewall
- fail2ban
- chrony
- SSH settings
- PAM limits
- systemd limits
- installed packages
- microcode packages
- summaries
- backups
- logs

## Run Verification

```bash
bash /root/ubuntu22-verify.sh
```

## Useful Manual Checks

```bash
swapon --show
free -h
ulimit -n
ufw status verbose
systemctl status fail2ban --no-pager
chronyc tracking
timedatectl
```

---

# Repository Structure

```text
ubuntu-server-22.04-baseline/
├── CHANGELOG.md
├── README.md
├── docs/
│   ├── limits.md
│   └── recovery.md
├── setup/
│   └── ubuntu22-system-setup.sh
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

---

# Recommended Workflow

1. Run dry-run first
2. Review hostname, swap, limits, firewall ports, SSH choices, and password selections
3. Run apply mode
4. Complete password prompts during apply mode
5. Open a second terminal
6. Verify the new sudo admin SSH login works
7. Run the generated verification script
8. Reboot server
9. Rerun verification after reboot

---

# Recovery

See:

```text
docs/recovery.md
```

---

# Limits Reference

See:

```text
docs/limits.md
```
