# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 baseline for provisioning, hardening, tuning, verification, reusable configuration, update management, and optional WireGuard support.

Current baseline version:

```text
v1.6.1
```

---

## v1.6.1 Hotfix

This release fixes the silent-exit issue found during real server testing.

The previous script could stop while creating a new system tuning file and never reach the final verification-script creation step.

Fixed in this release:

- Missing source files are no longer treated as failed backups.
- Dry-run command wrappers now return success cleanly.
- Future script failures now print the failing line and command.
- Successful apply runs create `/root/ubuntu22-verify.sh`.

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
SCRIPT_VERSION="1.6.1"
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
2. Confirm the script version is `v1.6.1`.
3. Run dry-run mode.
4. Review the saved config.
5. Run apply mode.
6. Test the new admin login from a second terminal.
7. Confirm `/root/ubuntu22-verify.sh` exists.
8. Run verification.
9. Reboot if required.
10. Run verification again after reboot.

---

## Documentation

Additional docs:

```text
docs/recovery.md
docs/limits.md
docs/wireguard.md
```
