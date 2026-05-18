# Changelog

## v1.6.3

### Improved

- Improved WireGuard install-only reporting in the generated verification script.
- Improved WireGuard install-only reporting in the server summary.
- Verification now explains that no active WireGuard interface is expected when `WIREGUARD_MODE=install-only`.
- README now documents the microcode safety decision.

### Microcode Decision

The script continues to install the correct CPU microcode package for the detected CPU vendor.

If the opposite-vendor microcode package is also present, the script warns but does not automatically remove it.

Reason:

- keeping both packages is generally harmless
- the active CPU vendor determines which microcode is actually used
- removing the opposite package may remove kernel meta-packages on some systems
- warning-only behavior is safer for production fleet provisioning

---

## v1.6.2

### Fixed

- Fixed generated verifier failure during package checks.
- Fixed `binary: unbound variable` caused by dpkg format strings being interpreted by Bash.
- Reworked verifier package checks to use direct `dpkg-query` commands.
- Added noninteractive `needrestart` behavior to update and install commands where applicable.

### Improved

- More reliable `/root/ubuntu22-verify.sh` execution.
- Cleaner package verification output.
- Reduced prompts during package install/update operations.

---

## v1.6.1

### Fixed

- Fixed silent script exits found during real server testing.
- Fixed `backup_file()` returning non-zero when there was no existing file to back up.
- Fixed dry-run command wrapper behavior so dry-run returns success cleanly.
- Added an error trap so future failures print the failing line and command.
- Fixed the first-run path where the script stopped before creating `/root/ubuntu22-verify.sh`.

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
