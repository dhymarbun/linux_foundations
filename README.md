# Linux Foundations

> Building a Linux administration foundation for Blue Team and Security Operations Center (SOC) roles.

## Overview

This repository documents my hands-on Linux administration journey using a dedicated Ubuntu Server running on an old ASUS VivoBook. The server is remotely administered from a Kali Linux workstation over SSH and serves as the foundation of my personal cybersecurity homelab.

Instead of only learning commands, every lab focuses on understanding how Linux systems behave, how services communicate, and how to investigate them from both an administrator's and an attacker's perspective.

---

## Homelab Architecture

```text
Windows 11 Host
│
├── Kali Linux VM
│      │
│      └── SSH
│
└──────────────► Ubuntu Server (Node-01)
```

---

## Hardware

| Component | Specification             |
| --------- | ------------------------- |
| Device    | ASUS VivoBook X441B       |
| CPU       | AMD A4-9125               |
| RAM       | 4 GB DDR4                 |
| Storage   | 256 GB SSD                |
| OS        | Ubuntu Server 24.04.4 LTS |

---

## Objectives

* Build solid Linux administration skills
* Learn networking fundamentals
* Understand Linux services and processes
* Practice SSH administration
* Develop system troubleshooting skills
* Prepare for SOC Analyst responsibilities
* Build a documented cybersecurity portfolio

---

## Completed Labs

### Lab 001 — Deploy Node-01

Completed:

* Installed Ubuntu Server 24.04.4 LTS
* Configured networking
* Enabled SSH
* Connected remotely from Kali Linux
* Updated system packages
* Verified exposed services using Nmap
* Compared internal (`ss`) and external (`nmap`) network visibility

---

## Skills Demonstrated

* Linux Installation
* Remote Administration (SSH)
* Network Configuration
* Service Enumeration
* Basic Reconnaissance
* Linux Package Management
* Troubleshooting

---

## Roadmap

* [x] Ubuntu Server Installation
* [x] SSH Remote Access
* [ ] Linux Filesystem
* [ ] Users & Permissions
* [ ] systemd Services
* [ ] Log Analysis
* [ ] Bash Scripting
* [ ] Firewall (UFW)
* [ ] Fail2Ban
* [ ] Networking Fundamentals
* [ ] Docker
* [ ] Wazuh Integration

---

**This repository is part of my cybersecurity learning journey toward a Security Operations Center (SOC) Analyst role.**
