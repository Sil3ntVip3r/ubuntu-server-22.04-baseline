# Recovery Notes

## Console Recovery

If SSH access is lost:

1. Use VPS provider web console
2. Boot into recovery/rescue if required
3. Mount root filesystem
4. Edit:

```bash
/etc/ssh/sshd_config
```

Temporarily set:

```text
PermitRootLogin prohibit-password
PasswordAuthentication yes
```

Then:

```bash
sshd -t
systemctl restart ssh
```

## Verify SSH Access

Always test:

```bash
ssh admin@server-ip
sudo whoami
```

Expected:

```text
root
```

before closing existing root sessions.
