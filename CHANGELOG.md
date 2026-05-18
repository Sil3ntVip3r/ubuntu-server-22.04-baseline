# Changelog

## v1.5.1

### Fixed

- Fixed generated verification script variable expansion issues.
- Fixed `$2: unbound variable` verification failures.
- Verification script now safely executes nested shell checks.

### Security / Safety Improvements

- Removed dangerous automatic microcode package removal behavior.
- Baseline now avoids accidental removal of kernel meta-packages.
- Opposite-vendor microcode packages are now WARNED about instead of automatically removed.

### Microcode Safety Change

Previous behavior:

- Intel systems removed `amd64-microcode`
- AMD systems removed `intel-microcode`

New safer behavior:

- Correct microcode package is installed automatically.
- Opposite microcode package is left installed unless manually reviewed.
- Script warns administrators to manually simulate package removal before cleanup.

### Recommended Manual Validation

Example:

```bash
sudo apt remove --simulate amd64-microcode
```

or:

```bash
sudo apt remove --simulate intel-microcode
```

Only remove the package if NO kernel meta-packages would also be removed.

### Improved

- Safer production deployment behavior.
- Better kernel package protection.
- More reliable verification reporting.
- Improved fleet safety.

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

### Ubuntu Update Policy

The baseline now:

- installs Ubuntu 22.04 security updates
- installs Ubuntu 22.04 package updates
- installs kernel/security patches
- blocks Ubuntu release upgrades
- prevents accidental 22.04 -> 24.04 upgrades

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

- Interactive swap sizing
- Auto-recommended swap size calculation based on RAM and server role
- Custom swap size entry support
- Swap validation for G/M suffixes
- Swap size recorded in server summary

---

## v1.0.0

Initial fleet-ready Ubuntu 22.04 baseline.
