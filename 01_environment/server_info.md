# Server Information — Stage 1 (Mava, solo)

## Connection

| Field             | Command                      | Value                                                     |
| ----------------- | ---------------------------- | --------------------------------------------------------- |
| Server IP (host)  | `ip addr`                    | 127.0.0.1 (localhost via port forward)                    |
| SSH port (host)   | QEMU hostfwd config          | 2222 (guest port 22)                                      |
| Guest internal IP | `ip addr`                    | 10.0.2.15 (interface ens3, QEMU user network 10.0.2.0/24) |
| SSH username      | —                            | mava                                                      |
| Connection method | `ssh -p 2222 mava@localhost` | Key-based SSH to localhost:2222                           |
| Authentication    | —                            | SSH key-based (Ed25519), no password                      |
| Private key       | —                            | Not stored in repository                                  |

## System

| Field      | Command          | Value                                                  |
| ---------- | ---------------- | ------------------------------------------------------ |
| OS         | `lsb_release -a` | Ubuntu 22.04.5 LTS (jammy)                             |
| Kernel     | `uname -a`       | 5.15.0-203-generic x86_64                              |
| vCPUs      | `nproc`          | 2 (Intel Core i7-9750H @ 2.60GHz)                      |
| RAM        | `free -h`        | 1.9 GiB total (2 GB assigned to VM)                    |
| Disk       | `df -h /`        | 20 GB (/dev/sda1), 1.7 GiB used, 18 GiB available (9%) |
| Hypervisor | —                | QEMU/KVM (local VM)                                    |

## Services

| Field              | Command                     | Value                        |
| ------------------ | --------------------------- | ---------------------------- |
| SSH (sshd)         | `systemctl is-active sshd`  | active                       |
| SSH (sshd enabled) | `systemctl is-enabled sshd` | alias                        |
| sudo               | `sudo -n true`              | passwordless for user `mava` |
| User groups        | `groups`                    | mava, sudo, docker           |

## Notes

- Provisioned by Mava (Stage 1 solo owner per TASKS.md).
- No passwords, private SSH keys, or secrets stored in this file.
- VM networking uses QEMU user-mode (`-netdev user`) with `hostfwd=tcp::2222-:22`.
