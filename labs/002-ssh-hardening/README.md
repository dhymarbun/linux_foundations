# Lab 002 - SSH Hardening & Public Key Authentication

## Objective

The objective of this lab was to understand how SSH authentication works, configure SSH public key authentication, and harden an Ubuntu Server by disabling password-based authentication after verifying secure key-based access.

---

# Environment

| Component      | Description             |
| -------------- | ----------------------- |
| Client         | Kali Linux              |
| Server         | Ubuntu Server 24.04 LTS |
| Authentication | ED25519 SSH Key Pair    |
| Network        | Private Local Network   |

---

# Skills Demonstrated

* Linux System Administration
* SSH Administration
* SSH Key Management
* Linux Configuration
* Authentication Troubleshooting
* Security Hardening

---

# Concepts Learned

## Linux Filesystem

| Directory  | Purpose                    |
| ---------- | -------------------------- |
| `/etc`     | System configuration files |
| `/home`    | User home directories      |
| `/var/log` | System logs                |
| `/bin`     | Essential binaries         |
| `/tmp`     | Temporary files            |

---

## SSH Architecture

### SSH Client

The SSH client initiates a connection to a remote machine.

### SSH Server (`sshd`)

The SSH daemon listens for incoming connections, authenticates clients, and provides remote shell access.

---

## Authentication Methods

### Password Authentication

Authentication is performed using a username and password.

**Advantages**

* Simple to configure.

**Disadvantages**

* Susceptible to brute-force attacks.
* Password reuse.
* Weak password policies.

---

### Public Key Authentication

Authentication is performed using asymmetric cryptography.

Private key:

```text
~/.ssh/id_ed25519
```

Stored only on the client.

Public key:

```text
~/.ssh/authorized_keys
```

Stored on the server.

The private key never leaves the client machine.

---

# Investigation

## Problem

SSH authentication always prompted for a password.

---

## Hypothesis

The client machine did not possess a valid SSH private key.

---

## Evidence

Verbose SSH output showed:

```text
Trying private key...
type -1
Next authentication method: password
```

This indicated that the SSH client attempted public key authentication but could not locate a valid private key.

---

## Root Cause

No ED25519 SSH key pair existed on the Kali client.

---

# Implementation

## Generate an ED25519 Key Pair

```bash
ssh-keygen -t ed25519
```

Generated files:

```text
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

---

## Install the Public Key

```bash
ssh-copy-id username@192.168.x.x
```

The public key was copied to:

```text
~/.ssh/authorized_keys
```

on the Ubuntu server.

---

## Verify Authentication

```bash
ssh -v username@192.168.x.x
```

Successful authentication:

```text
Offering public key
Server accepts key
Authenticated using "publickey"
```

---

## Harden SSH

Modified:

```text
/etc/ssh/sshd_config
```

Changed:

```text
PasswordAuthentication no
```

Validate configuration:

```bash
sudo sshd -t
```

Reload the SSH daemon:

```bash
sudo systemctl reload ssh
```

A second SSH session was opened to verify successful authentication before closing the original session.

---

# Commands Learned

## Navigation

```bash
pwd
ls
cd
```

---

## Searching

Locate files:

```bash
find
```

Search inside files:

```bash
grep
```

Examples:

```bash
find /etc -name sshd_config
grep PasswordAuthentication /etc/ssh/sshd_config
grep -v '^#' /etc/ssh/sshd_config
```

---

## SSH

```bash
ssh
ssh -v
ssh-keygen
ssh-copy-id
```

---

## Service Management

```bash
sudo sshd -t
sudo systemctl reload ssh
```

---

# Verification Checklist

* [x] Generated an ED25519 SSH key pair
* [x] Installed the public key on the Ubuntu server
* [x] Verified successful public key authentication
* [x] Disabled password authentication
* [x] Validated the SSH configuration
* [x] Reloaded the SSH daemon safely
* [x] Successfully logged in without using a password

---

# Screenshots

The following screenshots are included with this lab:

| Screenshot       | Description                                                                                        |
| ---------------- | -------------------------------------------------------------------------------------------------- |
| `generated_keys` | Generated ED25519 SSH key pair in the client's `~/.ssh` directory.                                 |
| `publickey`      | Successful SSH authentication using public key authentication (`Authenticated using "publickey"`). |
| `sshd_config`    | SSH server configuration showing `PasswordAuthentication no`.                                      |
| `config_valid`   | Validation of the SSH configuration using `sudo sshd -t` before reloading the SSH daemon.          |

> **Note:** Sensitive information such as private IP addresses, SSH fingerprints, usernames, and key contents has been redacted from the screenshots.

---

# Lessons Learned

This lab emphasized the importance of investigating before modifying a production service.

The workflow followed throughout the lab was:

1. Investigate
2. Form a hypothesis
3. Gather evidence
4. Identify the root cause
5. Implement the solution
6. Validate the configuration
7. Verify the result

Using this workflow helps reduce configuration mistakes and reflects best practices in Linux system administration and cybersecurity.
