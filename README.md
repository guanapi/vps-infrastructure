# Code Factory, Cloud Infrastructure & Linux Hardening

Public documentation of our VPS setup, security hardening, and agent-ready infrastructure.

> [!NOTE]
> All host-specific values (IPs, usernames, keys, OCIDs, and tokens) are intentionally omitted or replaced with `<PLACEHOLDERS>` for public safety.

## Project Goals

This is a code factory project built with a senior developer friend to:

1. Learn how to configure and work with AI agents effectively.
2. Gain hands-on experience with AI workflows and Linux infrastructure.
3. Put theory into practice by building and hardening a production-like server.
4. Explore building apps that can generate passive income or new business opportunities.

## Stack Overview

| Component | Configuration |
|-----------|---------------|
| **Cloud** | Oracle Cloud Infrastructure (OCI Compute) — Always Free Tier (ARM 2 OCPU + 12 GB RAM) |
| **OS** | Ubuntu 26.04.1 LTS |
| **Network** | Tailscale mesh VPN; public inbound ports closed (`<VERIFY_UFW_STATE>`) |
| **Auth** | SSH key-pair with passphrase (password login disabled) |
| **Services** | Telegram bot (`<TODO: add runtime/isolation details>`) |

---

## Network & Firewall

- **Tailscale:** `<TODO: document how Tailscale is configured and how SSH is restricted to the Tailscale interface/IP>`
- **UFW:** `<TODO: document default policies and allowed rules, without exposing real IPs>`
- **Fail2ban:** `<TODO: document enabled jails and ban policies>`

---

## OS Hardening & Security

### SSH Access & `sshd_config`

- Created a dedicated SSH users group (`<SSH_GROUP_NAME>`) to restrict who can log in over SSH.
- Removed short Diffie-Hellman moduli (`/etc/ssh/moduli`) to prevent weak key exchange.
- Hardened `/etc/ssh/sshd_config`:

| Setting / Goal | Purpose |
|----------------|---------|
| `AllowGroups <SSH_GROUP_NAME>` | Restrict SSH access to authorized users only |
| `PermitRootLogin no` | Disable direct root login |
| `PasswordAuthentication no` | Disable password login to prevent brute-force attacks |
| `PermitUserEnvironment no` | Prevent users (especially agents) from setting environment variables |
| `AllowTcpForwarding no` | Disable TCP port forwarding |
| `AllowAgentForwarding no` | `<TODO: confirm if agent forwarding is also disabled>` |
| `X11Forwarding no` | Disable X11 graphical forwarding |
| `UseDNS yes` | Verify remote hostname matches IP |
| `TCPKeepAlive no` | Disable TCP keepalive spoofing vector |
| `ClientAliveCountMax 3` | Disconnect unresponsive/idle SSH sessions after 3 missed checks |
| `ListenAddress <TAILSCALE_IP>` | Bind SSH only to the private Tailscale IP |
| `MaxSessions 2` | Limit concurrent sessions per connection |
| `MaxStartups 10:30:60` | Rate-limit concurrent unauthenticated connections |

### Privilege Escalation & Time Sync

- **Restricted `sudo` and `su`:** Limited to privileged groups only, isolating what both human users and AI agents can execute.
- **NTP:** Configured time synchronization so security protocols, logs, and certificates rely on accurate system time.

### Automatic Security Updates & Alerts

- Configured `unattended-upgrades` to automatically install critical security patches.
- Configured email notifications to alert on updates/issues (`<TODO: document mail relay/alerting tool without exposing email/credentials>`).

---

## Services

### Telegram Bot

- `<TODO: how it runs (systemd / Docker / user isolation)>`
- `<TODO: how secrets are injected (e.g., .env excluded via .gitignore)>`

---

## Documentation Progress

- [x] Project goals & stack overview
- [x] SSH hardening (`sshd_config`, SSH group, DH moduli)
- [x] `sudo`/`su` restrictions & NTP
- [x] Unattended upgrades & email alerts
- [ ] Tailscale + UFW rules (reconcile public port status)
- [ ] Fail2ban configuration
- [ ] Telegram bot deployment & isolation
- [ ] Backup & recovery strategy
