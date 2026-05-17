# Ubuntu Server 22.04 Baseline

Fleet-ready Ubuntu 22.04 provisioning and hardening baseline for VPS, blockchain, Docker, and infrastructure servers.

## Features

- 20GB swap provisioning
- SSH hardening
- Admin sudo user provisioning
- UFW + Fail2Ban
- Chrony time synchronization
- System tuning and limits
- BBR networking
- SSD/NVMe optimization
- Verification scripts
- Logging and summaries
- Convergent/idempotent design

## Usage

Dry run:

```bash
sudo bash ubuntu22-system-setup.sh
```

Apply:

```bash
sudo bash ubuntu22-system-setup.sh --apply
```
