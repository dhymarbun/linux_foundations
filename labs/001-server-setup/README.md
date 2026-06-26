# Lab 001 — Deploy Node-01

## Objective

Deploy a dedicated Ubuntu Server that will act as the primary Linux server for my cybersecurity homelab.

---

## Environment

**Operating System**

Ubuntu Server 24.04.4 LTS

**Hardware**

* ASUS VivoBook X441B
* AMD A4-9125
* 4 GB RAM
* 256 GB SSD

---

## Activities

* Installed Ubuntu Server
* Configured network connectivity
* Updated installed packages
* Installed OpenSSH Server
* Connected remotely from Kali Linux
* Performed initial service enumeration

---

## Validation

Verified remote connectivity using:

* SSH
* Nmap
* ss
* ping

Observed that only TCP port 22 (SSH) was exposed externally.

---

## Lessons Learned

* Difference between internal (`ss`) and external (`nmap`) service visibility.
* Importance of establishing a baseline after deploying a server.
* Basic Linux networking and remote administration.
* Initial troubleshooting of Ubuntu Server installation and networking.

---

## Next Steps

* Configure SSH key authentication
* Harden SSH configuration
* Configure UFW
* Begin Linux filesystem exploration
