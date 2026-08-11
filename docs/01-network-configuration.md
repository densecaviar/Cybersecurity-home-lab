# Phase 1 - Network Configuration

## Summary

This phase establishes the network foundation for the cybersecurity home lab. The objective is to assign consistent network identities to each system using static IPv4 addresses, verify connectivity between hosts, and prepare the environment for secure remote administration in subsequent phases.

## Objective

Configure reliable network communication between all three physical machines by assigning static IP addresses and verifying end-to-end connectivity across the local network.

## Rationale

Security tools such as SSH, Nmap, Hydra, and Wireshark rely on predictable network communication. Dynamic IP addresses assigned by DHCP (Dynamic Host Configuration Protocol) may change over time, making automation and documentation difficult.

Static addressing ensures each host can always be reached at the same address throughout the project.

## Environment
```
  HOST    ROLE       OPERATING SYSTEM      STATIC IP ADDRESS
| Odin  | Observer | macOS               | 192.168.1.20      |
| Atlas | Target   | Debian              | 192.168.1.7       |
| Hades | Attacker | Kali Linux          | 192.168.1.18      |
```

## Implementation
### Identify existing Network Configuration

Before configuring static IP addresses, the existing network configuration was examined on each host to determine the active network interface and the currently assigned IPv4 address.

Since Atlas and Hades will function as remote systems administered over SSH, they require consistent IP addresses throughout the project. Predictable addressing simplifies remote administration, automation, and documentation.

Odin, the observer workstation, does not require inbound SSH connections and therefore does not require manual static IP configuration. It communicates with the other hosts using their fixed addresses.
<pre>
To verify Atlas's current network configuration, the following command was executed:
```bash
ip addr
```
Why this command?

The `ip addr` command displays all network interfaces and their assigned IPv4 and IPv6 addresses. This allows the active interface and its current address to be identified before any configuration changes are made.

Example output:
```text
inet 192.168.1.7/24
```
The output confirmed that Atlas was currently using the address 192.168.1.7.

## Configure a Static IPv4 Address

Atlas uses Debian Linux, which supports traditional interface configuration through the /etc/network/interfaces file.

The configuration file was opened using:
`sudo nano /etc/network/interfaces`

The network interface was then configured with a fixed IPv4 address to ensure Atlas consistently uses the same address across reboots.
</pre>

## Verification

After applying the network configuration, connectivity between the laboratory systems was verified using ICMP echo requests.

Successful communication was confirmed between:

- Odin and Atlas
- Odin and Hades
- Atlas and Hades
- Each host and the default gateway

The configured IP addresses remained consistent following a system reboot, confirming that the static configuration was applied successfully.

## Lessons Learned
