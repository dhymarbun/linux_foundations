# Lab 002 - SSH Hardening & Public Key Authentication
27/06/2026 

## Objective

The goal of this lab was to understand how SSH authentication works, migrate from password-based authentication to public key authentication, and safely harden an Ubuntu Server without losing remote access.

---

# Environment

| Component      | Description                         |
| -------------- | ----------------------------------- |
| Client         | Kali Linux                          |
| Server         | Ubuntu Server 24.04 LTS             |
| Authentication | ED25519 SSH Key                     |
| Connection     | Local Network (Private IP Redacted) |

---

# Concepts Learned

## Linux Filesystem

Common directories used throughout the lab:

| Directory  | Purpose                        |
| ---------- | ------------------------------ |
| `/etc`     | System configuration files     |
| `/home`    | User home directories          |
| `/var/log` | System and authentication logs |
| `/bin`     | Essential binaries             |
| `/tmp`     | Temporary files                |

---

## SSH Client vs SSH Server

### SSH Client

The SSH client initiates a remote connection to another machine.

### SSH Server (sshd)

The SSH daemon waits for incoming connections, authenticates clients, and grants remote access.

---

## Password Authentication

The client authenticates using a username and password.

Advantages:

* Easy to configure.

Disadvantages:

* Vulnerable to brute-force attacks.
* Password reuse.
* Weak passwords.

---

## Public Key Authentication

Instead of proving knowledge of a password, the client proves ownership of a private key.

### Private Key

Stored only on the client machine.

```
~/.ssh/id_ed25519
```

### Public Key

Copied to the server and stored inside:

```
~/.ssh/authorized_keys
```

This allows the server to verify the client without ever receiving the private key.

---

# Investigation

## Problem

SSH connections always requested a password.

## Hypothesis

The client did not possess a valid SSH private key.

## Evidence

Verbose SSH output (`ssh -v`) showed:

```
Trying private key...
type -1
Next authentication method: password
```

The SSH client attempted to use a private key but could not find one in the default location.

## Root Cause

No ED25519 private key existed on the Kali client.

---

# Implementation

## Generate a New SSH Key Pair

```bash
ssh-keygen -t ed25519
```

Generated:

```
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

---

## Install the Public Key

```bash
ssh-copy-id username@192.168.x.x
```

The command copied the public key into:

```
~/.ssh/authorized_keys
```

on the Ubuntu server.

---

## Verify Authentication

```bash
ssh -v username@192.168.x.x
```

Evidence:

```
Offering public key
Server accepts key
Authenticated using "publickey"
```

This confirmed that password authentication was no longer required.

---

## Harden SSH

Modified:

```
/etc/ssh/sshd_config
```

Changed:

```
PasswordAuthentication no
```

Validate configuration:

```bash
sudo sshd -t
```

Apply changes safely:

```bash
sudo systemctl reload ssh
```

A new SSH session was opened to verify successful authentication before closing the existing session.

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

* [x] Generated an ED25519 SSH key pair.
* [x] Installed the public key on the Ubuntu server.
* [x] Verified SSH public key authentication.
* [x] Disabled password authentication.
* [x] Validated SSH configuration.
* [x] Reloaded the SSH daemon successfully.
* [x] Confirmed successful login without a password.

---

# Screenshots

Include the following screenshots:

1. Successful SSH authentication using a public key.
2. `PasswordAuthentication no` inside `sshd_config`.
3. `sudo sshd -t` validation.
4. `ls ~/.ssh` showing the generated key pair.
5. Successful SSH login without a password prompt.

Sensitive information has been intentionally redacted from screenshots, including:

* Private IP addresses
* SSH fingerprints
* Public key contents
* Personal hostnames (optional)

---

# Lessons Learned

This lab emphasized investigation before modification.

The workflow followed throughout the exercise was:

1. Investigate
2. Form a hypothesis
3. Collect evidence
4. Identify the root cause
5. Implement the solution
6. Validate the configuration
7. Verify the final result

Rather than relying on trial and error, each configuration change was supported by evidence gathered from the system. This approach minimizes configuration mistakes and reflects real-world Linux system administration and cybersecurity practices.
