## Summary

Configure secure remote administration for the laboratory using OpenSSH and ED25519 public key authentication. Password-based authentication is initially used to establish trust before transitioning to passwordless authentication using asymmetric cryptography. This phase also explains the underlying cryptographic concepts behind SSH authentication and secure communication.

## Objective

Install and configure OpenSSH
Verify remote SSH connectivity
Generate an ED25519 key pair
Install the public key on remote hosts
Configure passwordless authentication
Simplify administration using SSH client configuration
Understand how SSH authentication differs from SSH encryption

## Rationale

Remote administration is a fundamental component of Linux system administration and cybersecurity. Rather than physically interacting with each machine, administrators securely manage systems across a network using Secure Shell (SSH).

Although passwords can authenticate users, they become inconvenient when managing multiple systems and are susceptible to brute-force attacks.

SSH public key authentication replaces repeated password entry with asymmetric cryptography. A private key remains securely stored on the client, while its corresponding public key is installed on trusted servers. During authentication, the client proves ownership of the private key without ever transmitting it across the network.

Once authentication succeeds, SSH establishes an encrypted session using a symmetric session key, providing both security and performance.

## Concepts

### Authentication vs Encryption
One of the most common misconceptions about SSH is that the generated ED25519 key pair encrypts the entire SSH session.

In reality, the ED25519 key pair is used primarily for **authentication**.

The client proves ownership of its private key by digitally signing a challenge sent by the server. The server verifies this signature using the stored public key located inside the `authorized_keys` file.

After both parties have authenticated one another, SSH performs a secure key exchange (typically using Curve25519 / ECDH) to derive a shared symmetric session key.

All subsequent communication is encrypted using fast symmetric algorithms such as AES or ChaCha20 rather than repeatedly using public-key cryptography.

This design combines the strong identity verification provided by asymmetric cryptography with the speed and efficiency of symmetric encryption.

## Implementation

### Install OpenSSH Server

The OpenSSH server was installed on both Atlas and Hades to enable secure remote administration.

```bash
sudo apt update
sudo apt install openssh-server
```

#### Why this command?

The `openssh-server` package installs the SSH daemon (`sshd`), allowing the machine to securely accept incoming SSH connections.

After installation, the service was verified using:

```bash
sudo systemctl status ssh
```
A successful installation displays:

```text
Active: active (running)
```
### Verify SSH Connectivity

Before configuring key-based authentication, SSH connectivity was verified using password authentication.

From Odin:

```bash
ssh target@192.168.1.7
```

```bash
ssh attacker@192.168.1.18
```

#### Why this step?

Verifying password-based authentication first confirms:

- The SSH daemon is running correctly.
- Network connectivity exists between hosts.
- Firewall rules permit SSH traffic.
- User credentials are valid.

Establishing successful password authentication ensures the environment is functioning correctly before introducing public key authentication.

### Generate an ED25519 Key Pair

On Odin, an ED25519 key pair was generated using:

```bash
ssh-keygen -t ed25519 -C "observer@odin"
```

#### Why this command?

- `ssh-keygen` generates SSH key pairs.
- `-t ed25519` specifies the Ed25519 elliptic curve signature algorithm.
- `-C` attaches a descriptive comment to identify the key.

The command generates two files:

```text
~/.ssh/id_ed25519
```

Private key

```text
~/.ssh/id_ed25519.pub
```

Public key 

The private key always remains on Odin and is never transmitted across the network.

The public key can be safely copied to any trusted server that should accept authentication from this workstation.

#### Why ED25519?

ED25519 is a modern elliptic curve digital signature algorithm that provides:

- Strong cryptographic security
- Small key sizes
- Fast authentication
- Excellent performance
- Broad OpenSSH support

Compared to older RSA keys, ED25519 offers improved performance while maintaining a high level of security.

### Install the Public Key

The generated public key was copied to Atlas and Hades.

```bash
ssh-copy-id target@192.168.1.7
```

```bash
ssh-copy-id attacker@192.168.1.18
```

#### Why this command?

`ssh-copy-id` securely copies the client's public key to the remote user's `authorized_keys` file.

This operation requires the user's password only once to establish initial trust.

After installation, the server recognizes future authentication attempts from the corresponding private key without requiring the account password.

### Verify Passwordless Authentication

The SSH connection was tested again.

```bash
ssh target@192.168.1.7
```

Instead of requesting a password, the server authenticated the connection using the installed public key and granted access automatically.

At no point is the private key transmitted across the network.

The server simply verifies a cryptographic signature generated using the private key.


