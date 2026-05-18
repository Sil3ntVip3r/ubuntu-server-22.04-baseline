# Changelog

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

### Ubuntu Update Policy

The baseline now:

- installs Ubuntu 22.04 security updates
- installs Ubuntu 22.04 package updates
- installs kernel/security patches
- blocks Ubuntu release upgrades
- prevents accidental 22.04 -> 24.04 upgrades

### Added Configuration Options

```bash
RUN_SYSTEM_UPDATES=yes
ENABLE_UNATTENDED_SECURITY_UPDATES=yes
```

### Added Verification Checks

- release upgrade policy
- unattended-upgrades status
- reboot-required detection
- Ubuntu release validation

### Improved

- Better production fleet maintenance.
- Safer long-term patch management.
- More predictable server lifecycle handling.
- Improved security maintenance defaults.

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

### New Configuration Directory

```text
/root/system-setup-configs/
```

### New Usage Examples

Dry-run and save config:

```bash
sudo bash setup/ubuntu22-system-setup.sh
```

Apply and reuse latest config:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply
```

Apply with explicit config:

```bash
sudo bash setup/ubuntu22-system-setup.sh --apply --config /root/system-setup-configs/example.conf
```

---

## v1.3.1

### Fixed

- Fixed verification script awk escaping bug causing:

```text
ubuntu22-verify.sh: line XX: $2: unbound variable
```

- Verification script now properly validates installed packages.
- Improved generated verification output reliability.

### Improved

- CPU microcode handling now removes the incorrect vendor package.
- Intel systems now remove `amd64-microcode`.
- AMD systems now remove `intel-microcode`.
- Verification summaries now show installed microcode packages.

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

- Interactive swap sizing
- Auto-recommended swap size calculation based on RAM and server role
- Custom swap size entry support
- Swap validation for G/M suffixes
- Swap size recorded in server summary

---

## v1.0.0

Initial fleet-ready Ubuntu 22.04 baseline.
