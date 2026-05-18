# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 provisioning, hardening, tuning, verification, reusable configuration, and update-management baseline for:

- VPS infrastructure
- Blockchain and masternode servers
- Docker hosts
- RPC nodes
- Build servers
- General Ubuntu 22.04 infrastructure

Designed for repeatable fleet provisioning with convergent/idempotent configuration handling.

Current baseline version:

```text
v1.5.0
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
- Extra firewall ports
- Optional reboot

## Saved Configuration Workflow

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

# Ubuntu 22.04 Update Management

The baseline now includes safe Ubuntu 22.04 patch management.

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

This allows:

- normal Ubuntu 22.04 updates
- security patches
- kernel updates

while blocking:

- major Ubuntu release upgrades

## Safe Update Routine

The baseline safely runs:

```bash
apt update
apt upgrade -y
apt full-upgrade -y
apt autoremove -y
apt autoclean -y
```

## Unattended Security Updates

The baseline can automatically enable:

- security patch downloads
- unattended security upgrades
- package cleanup

Automatic rebooting is intentionally disabled by default.

This is safer for:

- blockchain nodes
- RPC nodes
- infrastructure servers
- Docker hosts

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
- saves reusable configuration files
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

- can reuse latest saved config
- can load explicit config files
- performs system changes
- writes configurations
- configures users
- installs/removes packages
- installs updates and security patches
- restarts services when needed
- securely prompts for passwords using Linux passwd

Passwords are:

- never logged
- never echoed
- never stored in variables
- never written to disk by the script

---

# Configuration Reuse

## Reuse Latest Config

When running apply mode, the script can automatically reuse the most recent saved config.

Example:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply
```

## Load Explicit Config

Example:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply --config /root/system-setup-configs/example.conf
```

## Example Config File

```bash
SERVER_HOSTNAME=node01
SERVER_ROLE=rpc-node
SERVER_LOCATION=OVH-Canada
ADMIN_USER=admin
SWAP_SIZE=20G
LIMIT_PROFILE=recommended
LIMIT_VALUE=500000
NPROC_VALUE=500000
FILE_MAX=2097152
ALLOW_PASSWORDLESS_SUDO=yes
SET_ADMIN_PASSWORD=yes
SET_ROOT_PASSWORD=yes
LOCK_ROOT_PASSWORD=no
RUN_SYSTEM_UPDATES=yes
ENABLE_UNATTENDED_SECURITY_UPDATES=yes
SSH_KEY_OPTION=2
EXTRA_TCP_PORTS=16113,80,443
EXTRA_UDP_PORTS=
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

## Firewall and Protection

- UFW firewall
- SSH port 22 automatically opened before firewall enablement
- Optional additional TCP/UDP ports
- Fail2Ban enabled

## CPU Microcode Handling

The script automatically installs the correct CPU microcode package and removes the incorrect vendor package.

### Intel CPUs

- installs `intel-microcode`
- removes `amd64-microcode`

### AMD CPUs

- installs `amd64-microcode`
- removes `intel-microcode`

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

The verification script is safe to rerun any time.

It validates:

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

## Useful Manual Checks

```bash
swapon --show
free -h
ufw status verbose
systemctl status fail2ban --no-pager
chronyc tracking
timedatectl
cat /etc/update-manager/release-upgrades
systemctl status unattended-upgrades --no-pager
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
9. Reboot server if updates/kernel changes require it
10. Rerun verification after reboot

---

# Recovery

See:

```text
docs/recovery.md
```
