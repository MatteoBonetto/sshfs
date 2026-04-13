# SSHFS on Windows and Linux

This guide explains how to mount a remote filesystem over SSH on Windows and Linux.

---

## 🪟 SSHFS on Windows

### 📦 Requirements

1. WinFsp: https://winfsp.dev  
2. SSHFS-Win: https://github.com/winfsp/sshfs-win/releases  

---

### 🚀 Setup

1. Install WinFsp  
2. Install SSHFS-Win  
3. Restart your system  

---

### 🔗 Mount

```
net use X: \\sshfs\user@host\path
```

Example:

```
net use X: \\sshfs\john@fileserver\home\john
```

---

### 🔐 Authentication

- Password (prompted)
- SSH keys (~/.ssh)

---

### 🔄 Reconnectable

```
net use X: \\sshfs.r\user@host\path
```

---

### 🧹 Unmount

```
net use X: /delete
```

---

## 🐧 SSHFS on Linux

### 📦 Install

Debian/Ubuntu:
```
sudo apt update
sudo apt install sshfs
```

Fedora:
```
sudo dnf install sshfs
```

Arch:
```
sudo pacman -S sshfs
```

---

### 📁 Create Mount Point

```
mkdir -p ~/mnt/remote
```

---

### 🔗 Mount

```
sshfs user@host:/remote/path ~/mnt/remote
```

Example:

```
sshfs john@fileserver:/home/john ~/mnt/remote
```

---

### ⚙️ Options

```
sshfs user@host:/remote/path ~/mnt/remote -o reconnect,ServerAliveInterval=15,ServerAliveCountMax=3
```

---

### 🧹 Unmount

```
fusermount -u ~/mnt/remote
```

Force:
```
fusermount -uz ~/mnt/remote
```

---

## 📚 Summary

- ssh → shell  
- scp/rsync → transfer  
- sshfs → mount filesystem  
