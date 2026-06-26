# Lab 001 - Ubuntu Server Deployment

## Objective

Deploy an Ubuntu Server to serve as the first node of my cybersecurity homelab.

---

## Environment

| Component | Value |
|-----------|-------|
| OS | Ubuntu Server 24.04.4 LTS |
| Host | ASUS VivoBook X441B |
| CPU | AMD A4-9125 |
| RAM | 10 GB |
| Access | SSH |

---

## Steps Performed

1. Installed Ubuntu Server.
2. Connected the server to the local network.
3. Enabled OpenSSH Server.
4. Verified SSH was listening on TCP port 22.
5. Connected remotely from a Kali Linux workstation.
6. Verified the service externally using Nmap.

---

## Validation

### Network

![Network](screenshots/network.png)

---

### SSH Service

![SS](screenshots/ss.png)

---

### External Verification

![Nmap](screenshots/nmap.png)

---

### Remote Login

![SSH](screenshots/ssh.png)

---

## Lessons Learned

- Difference between internal (`ss`) and external (`nmap`) service verification.
- Difference between listening sockets and firewall exposure.
- Basic SSH remote administration.
- Ubuntu Server networking fundamentals.

---

## Status

✅ Successful
