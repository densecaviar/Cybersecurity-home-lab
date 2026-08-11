# Phase 1 - Network Configuration

## Summary

This phase establishes the network foundation for the cybersecurity home lab. The objective is to assign consistent network identities to each system using static IPv4 addresses, verify connectivity between hosts, and prepare the environment for secure remote administration in subsequent phases.

## Objective

Configure reliable network communication between all three physical machines by assigning static IP addresses and verifying end-to-end connectivity across the local network.

## Why do I need this?

Security tools such as SSH, Nmap, Hydra, and Wireshark rely on predictable network communication. Dynamic IP addresses assigned by DHCP (Dynamic Host Configuration Protocol) may change over time, making automation and documentation difficult.

Static addressing ensures each host can always be reached at the same address throughout the project.

## Environment

  HOST    ROLE       OPERATING SYSTEM      STATIC IP ADDRESS
| Odin  | Observer | macOS               | 192.168.1.20      |
| Atlas | Target   | Debian              | 192.168.1.7       |
| Hades | Attacker | Kali Linux          | 192.168.1.18      |

## Implementation
### Identify existing Network Configuration

Since I am using Odin only for SSH, I need not establish a static IP for this device. However, since I want to SSH into Atlas and Hades, I will have to make sure that I assign a static IP so that I can save it into a variable for quick automation.

Lets check Atlas's ip configuration first. Since it is a Debian server, I can run the command `ip addr` to check its current IP address.
It says `inet 192.168.1.7` for the wifi interface card its using. Now we can set this to a static address by altering the /etc/network/interfaces file. Using `nano /etc/network/interfaces` , I can now check the file and add a couple lines.  
and uses a legacy network configuration system instead of a network manager.





## Verification

## Lessons Learned
