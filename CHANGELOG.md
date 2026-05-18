# Changelog

## v1.6.1

### Fixed

- Fixed silent script exits found during real server testing.
- Fixed `backup_file()` returning non-zero when there was no existing file to back up.
- Fixed dry-run command wrapper behavior so dry-run returns success cleanly.
- Added an error trap so future failures print the failing line and command.
- Fixed the first-run path where the script stopped before creating `/root/ubuntu22-verify.sh`.

### Root Cause

`set -e` treated a missing backup source file as a fatal error. This caused the run to stop while creating new files such as:

```text
/etc/sysctl.d/99-custom-system-tuning.conf
```

### Improved

- Better first-run reliability.
- Clearer troubleshooting output.
- More reliable verification script generation.

---

## v1.6.0

### Added

- Optional WireGuard VPN support.
- Optional WireGuard package-only installation mode.
- Optional WireGuard simple server configuration mode.
- WireGuard interface configuration.
- WireGuard UFW UDP rule configuration.
- WireGuard service enablement.
- WireGuard verification checks.
- WireGuard reporting in server summaries.
- Dedicated WireGuard documentation.

Added:

```text
docs/wireguard.md
```

---

## v1.5.1

### Fixed

- Fixed generated verification script variable expansion issues.
- Fixed `$2: unbound variable` verification failures.
- Verification script now safely executes nested shell checks.
- Removed risky automatic opposite-vendor microcode package removal.
- Opposite-vendor microcode packages are now warned about instead of automatically removed.

---

## v1.5.0

### Added

- Safe Ubuntu 22.04 update and patch workflow.
- Automatic package update routine.
- Automatic package cleanup.
- Ubuntu release upgrade blocking.
- Unattended security updates configuration.
- Verification checks for release-upgrade policy.
- Verification checks for unattended-upgrades.
- Verification checks for reboot-required state.
- Config options for update management.
- Summary reporting for update configuration.

---

## v1.4.0

### Added

- Saved configuration workflow.
- Dry-run mode now automatically saves configuration files.
- Apply mode can reuse the latest saved configuration.
- Added `--config` support for explicit configuration loading.
- Added reusable fleet provisioning workflow.
- Added configuration summaries.
- Added configuration validation before apply.
- Added saved configuration tracking to summaries.
- Added verification checks for saved configs.

---

## v1.3.1

### Fixed

- Fixed verification script awk escaping bug causing:

```text
ubuntu22-verify.sh: line XX: $2: unbound variable
```

---

## v1.3.0

### Added

- Secure interactive password prompts for admin and root users.
- Dry-run mode password skipping.
- Dry-run password documentation.
- Separate admin password handling from passwordless sudo.
- Password selection tracking in summaries.

---

## v1.2.0

### Added

- System limits profiles.
- Conservative/recommended/max/custom limit selection.
- Custom limit validation.
- Limits profile logging and summaries.

---

## v1.1.0

### Added

- Interactive swap sizing.
- Auto-recommended swap size calculation based on RAM and server role.
- Custom swap size entry support.
- Swap validation for G/M suffixes.
- Swap size recorded in server summary.

---

## v1.0.0

Initial fleet-ready Ubuntu 22.04 baseline.
