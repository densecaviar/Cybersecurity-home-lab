# Cybersecurity-home-lab

# Overview
This project documents the design and implementation of a physical three-machine cybersecurity laboratory built to simulate a small enterprise environment.

**Why Physical Machines?**

Many cybersecurity home labs are implemented entirely within virtual machines on a single host. While virtualized labs are excellent learning environments, I chose to build this lab using three dedicated physical systems to gain hands-on experience with real networking, device configuration, and host-to-host communication.
Using separate machines allowed me to:

- Configure networking between independent hosts
- Practice secure remote administration using SSH
- Observe real network traffic between systems
- Simulate attacker, target, and observer roles
- Gain experience managing multiple operating systems simultaneously



This lab uses three dedicated physical systems with distinct operational roles:

 **Odin**    -    Observer and monitoring macOS workstation
 
 **Atlas**   -    Debian Linux target server
 
 **Hades**   -    Kali Linux attacker machine



# Lab Architecture
![Network Topology](images/network-topology.png)
# Objectives

- Design a segmented cybersecurity lab

- Configure secure SSH access using public key authentication
  
- Perform network reconnaissance

- Assess exposed services
  
- Harden Linux services
  
- Simulate common attacks
  
- Observe network traffic
  
- Document findings and mitigations






### Networking

- TCP/IP
- Static IPv4 Addressing
- SSH
- ED25519 Public Key Authentication

### Security Tools

- OpenSSH
- Nmap
- Hydra
- Wireshark
- UFW
- Fail2Ban

*(More tools will be added as the project progresses.)*

## Skills Demonstrated

This project demonstrates practical experience with:

- Linux Administration
- Network Configuration
- SSH Hardening
- Public Key Authentication
- Network Reconnaissance
- Vulnerability Assessment
- Password Auditing
- Network Traffic Analysis
- Security Documentation
- Incident Reporting



# Documents

- [Lab Setup](docs/01-lab-setup.md)
 
- [SSH Configuration](docs/02-ssh-configuration.md)
  
- [Network Reconnaissance](docs/03-network-reconnaissance.md)
  
- [Vulnerability Assessment](docs/04-vulnerability-assessment.md)
  
- [Password Auditing](docs/05-password-auditing.md)
  
- [Linux Hardening](docs/06-linux-hardening.md)
  
- [Traffic Analysis](docs/07-traffic-analysis.md)
  
- [Incident Report](docs/08-incident-report.md)
