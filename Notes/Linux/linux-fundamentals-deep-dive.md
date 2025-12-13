# 🐧 Linux Deep Dive: From User to Engineer

> **Status:** Learning in Progress 🚧
> **Focus:** Internals (File Systems, Networking, Virtualization).
> **Device:** ThinkPad (Arch Linux + i3wm) #IUseArchBTW

---

## 1. 📂 File System Hierarchy
Di Linux, mindset-nya harus diubah: **"Everything is a File"**.
Forget about "Drive C:" or "Drive D:". Semuanya start dari **Root (`/`)**.

### The Directory Map
| Path | Purpose | Example |
| :--- | :--- | :--- |
| **`/`** | **The Root**. Awal dari segalanya. *Don't mess up here.* | - |
| **`/home`** | **User Space**. Tempat nyimpen config (`.config`), *source code*, documents. | `/home/yui` |
| **`/etc`** | **Configuration Center**. System-wide settings ada di sini. | `/etc/pacman.conf`, `/etc/nginx/nginx.conf` |
| **`/var`** | **Variable Data**. Files yang ukurannya berubah-ubah (Logs, Databases, Spools). | `/var/log/syslog` |
| **`/bin`** | **Binaries**. Executables buat command dasar. | `/usr/bin/vim`, `/bin/ls` |
| **`/tmp`** | **Temporary**. File sampah sementara, *wiped out on reboot*. | - |

### Permissions & Security
Konsep dasar: **User**, **Group**, **Others**.
Actions: `r` (read), `w` (write), `x` (execute).

#### The Magic Numbers (chmod):
- **`777`** (rwx-rwx-rwx) 🚩 **DANGER ZONE**. Everyone can write/execute. Haram hukumnya di production server.
- **`755`** (rwx-r-x-r-x) ✅ Standard for **Directories/Scripts**. Owner bisa edit, public cuma bisa baca/run.
- **`644`** (rw-r--r--) ✅ Standard for **Config Files**. Owner bisa edit, public cuma bisa baca.

## 🌐 Networking Fundamentals
Masalah DevOps itu 50% adalah: "Why can't Service A talk too Service B?"

### Modern Tools
- **`Identity (Ip a)`**
- **`Listening Ports (ss -tuln)`**
- **`DNS Lookup (cat /etc/resolv.conf)`**

### SSH (Secure Shell)
Remote server wajib pakai Key-based Authentication (No Password)
- **`Public Key`** : The Padlock (Upload ke server)
- **`Private Key`** : The Key (Simpan aman di /home/yui/.ssh/id_rsa)

## 💻 Virtualization vs Containerization
Cara membagi resource hardware (CPU/RAM) ke banyak environment

### Virtual Machine (VM)
- **`Examples`** : KVM, VMware, VirtualBox
- **`Heavyweight`**
- **`Use Case`** : Full OS Isolation

### Containers (Docker)
- **`Examples`** : Docker, Podman
- **`Lightweight`**
- **`Use Case`** : Microservice, App deployment

## 4. 🤝 POSIX Compliance
**P**ortable **O**perating **S**ystem **I**nterface.
Standar biar script kita *portable* antar Unix-like systems (Linux, macOS, BSD).

* **The Rule:** Jangan terlalu bergantung sama fitur eksklusif `bash` kalau mau script-nya jalan di `sh` (Alpine Linux) atau `dash` (Ubuntu/Debian).
* **Tip:** Use `#!/bin/sh` for maximum portability, or `#!/bin/bash` if you really need specific features.

---

> *Notes written in Vim (Nord Theme).* ☕
