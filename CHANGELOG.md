# Changelog

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
