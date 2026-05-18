# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 baseline for provisioning, hardening, tuning, verification, reusable configuration, update management, and optional WireGuard support.

Current baseline version:

```text
v1.6.2
```

---

## v1.6.2 Hotfix

This release fixes the generated verifier package-check failure seen after `v1.6.1`.

The setup script completed correctly and created:

```text
/root/ubuntu22-verify.sh
```

but the verifier could fail during package checks with:

```text
binary: unbound variable
```

Fixed in this release:

- verifier package checks now avoid nested Bash expansion problems
- package verification uses direct `dpkg-query` commands
- the verifier no longer expands dpkg format strings as shell variables
- update/install commands use noninteractive `needrestart` behavior where applicable

---

## Previous v1.6.1 Fix

`v1.6.1` fixed the earlier silent-exit issue found during real server testing.

Fixed behavior:

- missing source files are no longer treated as failed backups
- dry-run command wrappers return success cleanly
- script failures print the failing line and command
- successful apply runs create `/root/ubuntu22-verify.sh`

---

## Main Features

- Interactive provisioning
- Saved dry-run configuration files
- Apply mode with saved config reuse
- Safe Ubuntu 22.04 package updates
- Ubuntu release-upgrade blocking
- Unattended security update support
- Swap configuration
- File and process limit profiles
- UFW firewall setup
- Fail2Ban setup
- Chrony time sync
- SSH hardening
- CPU microcode safety handling
- Optional WireGuard install/server mode
- Verification script generation
- Logs, backups, and summaries

---

## Usage

Clone the repository:

```bash
git clone https://github.com/Sil3ntVip3r/ubuntu-server-22.04-baseline.git
cd ubuntu-server-22.04-baseline
```

Update an existing clone:

```bash
git pull
grep SCRIPT_VERSION setup/ubuntu22-system-setup.sh
```

Expected:

```text
SCRIPT_VERSION="1.6.2"
```

Run dry-run mode:

```bash
sudo bash setup/ubuntu22-system-setup.sh
```

Run apply mode:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply
```

Run apply mode with a specific config:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply --config /root/system-setup-configs/example.conf
```

---

## Generated Files

Logs:

```text
/root/system-setup-logs/YYYYMMDD-HHMMSS/
```

Backups:

```text
/root/system-setup-backups/YYYYMMDD-HHMMSS/
```

Saved configs:

```text
/root/system-setup-configs/YYYYMMDD-HHMMSS.conf
```

Summary:

```text
/root/server-baseline-summary.txt
```

Verification script:

```text
/root/ubuntu22-verify.sh
```

Run verification:

```bash
bash /root/ubuntu22-verify.sh
```

---

## Recommended Workflow

1. Pull the latest repository.
2. Confirm the script version is `v1.6.2`.
3. Run apply mode again and reuse the saved config.
4. Confirm `/root/ubuntu22-verify.sh` exists.
5. Run verification.
6. Reboot if required.
7. Run verification again after reboot.

---

## Documentation

Additional docs:

```text
docs/recovery.md
docs/limits.md
docs/wireguard.md
```
