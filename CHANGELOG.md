# Changelog

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

### Security / Stability

- Cleaner CPU microcode management.
- Reduced unnecessary package overlap.
- Improved fleet consistency.

---

## v1.3.0

### Added

- Secure interactive password prompts for admin and root users.
- Dry-run mode password skipping.
- Dry-run password documentation.
- Separate admin password handling from passwordless sudo.
- Password selection tracking in summaries.

### Improved

- Clearer dry-run/apply workflow.
- Safer password handling design.
- Better production provisioning workflow.

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

### Auto Swap Recommendations

| Server Type / RAM | Recommended Swap |
|---|---|
| Small VPS (<=2GB RAM) | 4G |
| 4GB RAM | 4G |
| 8GB RAM | 8G |
| 16GB-32GB RAM | 16G |
| Blockchain / Docker / Build / RPC nodes | 20G |

---

## v1.0.0

Initial fleet-ready Ubuntu 22.04 baseline.

### Features

- Interactive server provisioning
- 20GB swap configuration
- SSH hardening
- Sudo admin user provisioning
- SSH key management
- UFW firewall
- Fail2Ban
- Chrony NTP
- Sysctl tuning
- File/process limits
- BBR networking
- SSD trim timer
- CPU microcode installation
- Verification script generation
- Summary and logging system
- Convergent/idempotent configuration handling
