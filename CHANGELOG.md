# Changelog

## v1.6.0

### Added

- Optional WireGuard VPN support.
- Optional WireGuard package-only installation mode.
- Optional WireGuard simple server configuration mode.
- Automatic WireGuard key generation.
- Automatic WireGuard interface configuration.
- Automatic WireGuard UFW UDP rule configuration.
- Automatic WireGuard service enablement.
- WireGuard verification checks.
- WireGuard reporting in server summaries.
- Dedicated WireGuard documentation.

### WireGuard Packages

The baseline can now install:

- wireguard
- wireguard-tools
- qrencode

### WireGuard Features

Optional server mode now supports:

- private key generation
- public key generation
- interface creation
- persistent configuration
- automatic service startup
- optional peer configuration

### Security Improvements

- WireGuard private keys are never stored in reusable config files.
- WireGuard private keys are never printed into logs.
- WireGuard configs are created with restrictive permissions.
- Key generation occurs locally on the target server.

### Documentation Improvements

Updated:

- README.md
- CHANGELOG.md
- verification references
- feature summaries

Added:

```text
docs/wireguard.md
```

### Future Expansion Path

WireGuard support creates a foundation for future:

- VPN-only management
- private RPC networking
- full mesh topologies
- fleet interconnects
- internal-only infrastructure

---

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

- Interactive swap sizing
- Auto-recommended swap size calculation based on RAM and server role
- Custom swap size entry support
- Swap validation for G/M suffixes
- Swap size recorded in server summary

---

## v1.0.0

Initial fleet-ready Ubuntu 22.04 baseline.
