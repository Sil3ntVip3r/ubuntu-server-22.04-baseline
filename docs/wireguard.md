# WireGuard Guide

This guide covers the optional WireGuard VPN functionality integrated into the Ubuntu Server 22.04 Baseline.

Reference:

urlWireGuard Official Sitehttps://www.wireguard.com/install/

---

# Purpose

WireGuard provides:

- encrypted server-to-server networking
- private management access
- private RPC connectivity
- VPN-only administration
- secure infrastructure communication

Recommended for:

- blockchain infrastructure
- RPC nodes
- Docker clusters
- VPS fleets
- remote management networks

---

# Supported Modes

## Install Only

Installs:

- wireguard
- wireguard-tools
- qrencode

without generating configs.

Useful when:

- configs are managed manually
- configs are deployed externally
- using Ansible/Terraform later

---

## Simple Server Mode

Automatically:

- generates WireGuard keys
- creates interface config
- opens UFW UDP port
- enables wg-quick service
- starts WireGuard interface

Generated files:

```text
/etc/wireguard/wg0.conf
/etc/wireguard/wg0.key
/etc/wireguard/wg0.pub
```

---

# Default Settings

| Setting | Default |
|---|---|
| Interface | wg0 |
| UDP Port | 51820 |
| VPN Network | 10.100.0.0/24 |
| Server Address | 10.100.0.1/24 |

---

# Security Design

The baseline intentionally:

- does NOT store WireGuard private keys in reusable config files
- does NOT print private keys into logs
- stores configs with restrictive permissions
- generates keys locally on the server

Permissions:

```text
/etc/wireguard/*.key -> 600
/etc/wireguard/*.conf -> 600
```

---

# Verify WireGuard

Check interface:

```bash
wg show
```

Check service:

```bash
systemctl status wg-quick@wg0
```

Check listening port:

```bash
ss -ulpn | grep 51820
```

Check firewall:

```bash
ufw status verbose
```

---

# Example Fleet Layout

| Server | VPN IP |
|---|---|
| node01 | 10.100.0.1 |
| node02 | 10.100.0.2 |
| node03 | 10.100.0.3 |

Potential future design:

- SSH only over WireGuard
- RPC only over WireGuard
- monitoring only over WireGuard
- private backend networking

---

# Future Planned Improvements

Potential future additions:

- automatic peer generation
- full mesh topology
- QR code client generation
- multi-peer management
- site-to-site support
- internal DNS
- private monitoring stack
- VPN-only firewall mode
