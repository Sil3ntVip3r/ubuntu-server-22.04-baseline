# Limits Profiles Reference

The Ubuntu 22.04 baseline supports selectable system limits profiles.

These profiles affect:

- open file descriptors (nofile)
- process limits (nproc)
- kernel file descriptor ceiling (fs.file-max)

The script applies limits through:

- /etc/security/limits.d/99-custom-limits.conf
- PAM limits integration
- systemd manager limits
- sysctl kernel tuning

---

# Conservative Profile

Recommended for:

- small VPS
- low-memory systems
- lightweight infrastructure

Settings:

nofile = 65535
nproc = 65535
fs.file-max = 1048576

---

# Recommended Profile

Recommended for:

- blockchain nodes
- Docker hosts
- RPC infrastructure
- general production servers

Settings:

nofile = 500000
nproc = 500000
fs.file-max = 2097152

This is the default recommended baseline.

---

# Max Profile

Recommended only for:

- high connection-count systems
- large Docker hosts
- heavy RPC workloads

Settings:

nofile = 1048576
nproc = 1048576
fs.file-max = 4194304

Use only if workloads justify it.

---

# Custom Profile

Allows fully custom:

- nofile
- nproc
- fs.file-max

Validation is performed before applying values.

---

# Verification

Check current limits:

ulimit -n
ulimit -u
sysctl fs.file-max

Check systemd manager limits:

systemctl show --property DefaultLimitNOFILE --property DefaultLimitNPROC

Check applied config files:

cat /etc/security/limits.d/99-custom-limits.conf
cat /etc/systemd/system.conf.d/99-custom-limits.conf
