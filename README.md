# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 baseline for provisioning, hardening, tuning, verification, reusable configuration, update management, and optional WireGuard support.

Current baseline version:

```text
v1.6.3
```

---

## v1.6.3 Update

This release improves WireGuard reporting and documents the microcode safety decision.

WireGuard install-only mode now reports clearly in both the server summary and verification script:

```text
WireGuard installed; no active interface detected. This is expected when WIREGUARD_MODE=install-only.
```

This avoids confusion when WireGuard packages are installed but no VPN interface is configured.

---

## Microcode Safety

The script installs the correct CPU microcode package for the detected CPU vendor.

If the opposite-vendor microcode package is also installed, the script warns but does not remove it automatically.

Reason:

- Removing the opposite microcode package can sometimes remove kernel meta-packages.
- Keeping both is generally harmless.
- The correct CPU microcode is selected by the system for the actual CPU vendor.
- Leaving both installed is safer than risking kernel package removal.

Manual cleanup should only be done after reviewing a simulated removal:

```bash
sudo apt remove --simulate amd64-microcode
sudo apt remove --simulate intel-microcode
```

Only remove a package if the simulation does not remove kernel meta-packages.

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
SCRIPT_VERSION="1.6.3"
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
2. Confirm the script version is `v1.6.3`.
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
