# Phase 5 - Linux Hardening

## Summary

This phase focuses on strengthening the security of `Atlas`, the Debian target server used in the cybersecurity home lab.

Unlike the previous SSH configuration phase, which focused primarily on establishing secure remote access, this phase focuses on reducing the attack surface of the Linux system and implementing additional security controls.

The hardening process follows a **baseline → modification → verification** approach. The existing configuration is first documented, security controls are then applied, and the system is subsequently tested to verify that the changes were successful.

---

## Objective

- Apply security updates and maintain current software
- Review user and privilege configuration
- Harden the SSH service
- Configure a host-based firewall
- Implement brute-force protection
- Identify and minimize unnecessary network services
- Review relevant security logs
- Re-scan the system to verify the effectiveness of the hardening measures

---

## Hardening Methodology

The hardening process will follow these stages:

1. Establish a security baseline.
2. Identify unnecessary exposure and weak configurations.
3. Apply appropriate security controls.
4. Verify that each control was successfully implemented.
5. Re-scan the system from `Hades`.
6. Compare the results against the original baseline.
7. Document the security improvements.

## 1. Establishing the Baseline

Before making any changes, the current configuration of Atlas was documented.
This provides a reference point for comparing the system before and after hardening.

### 1.1 Update the System

The package repositories were first updated:
``` bash
sudo apt update
```
![atlas updatable packages](../images/atlas-update.png)


`apt update` retrieves the latest package information from the configured Debian repositories.

The available package upgrades were then installed:
``` bash
sudo apt upgrade
```
![atlas upgradable packages](../images/atlas-upgrade.png)

`apt upgrade` installs available package updates.

Keeping the operating system and installed software updated is an important component of vulnerability management because security updates frequently contain patches for known vulnerabilities.

2. Review SSH Configuration

The effective SSH server configuration was examined using:
``` bash
sudo sshd -T
```


`sshd -T` displays the effective configuration used by the OpenSSH server after configuration files and defaults have been processed.
This provides a reliable way to audit the SSH configuration.
The output was reviewed to identify security-relevant settings such as:

Authentication methods,
Root login,
Password authentication,
Public key authentication,
Maximum authentication attempts,
and Protocol configuration.

## 3. Review Firewall Configuration

The current firewall configuration was checked using:
``` bash
sudo ufw status verbose
```

![firewall status](../images/firewall-status.png)

UFW (Uncomplicated Firewall) provides a simplified interface for managing Linux firewall rules.
The command displays whether the firewall is active and shows the currently configured rules.

4. Identify Listening Services
The services currently listening for network connections were identified using:
``` bash
sudo ss -tulpn
```
![network sockets](../images/network-sockets.png)

The ss command provides information about network sockets.

The options used here provide information about:

-t — TCP sockets
-u — UDP sockets
-l — Listening sockets
-p — Associated processes
-n — Display numerical addresses and ports

This allows the system's network attack surface to be examined.



