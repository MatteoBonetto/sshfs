# SSHFS on Windows

This guide explains how to mount a remote filesystem over SSH on Windows using **SSHFS-Win** and **WinFsp**.

---

## 📦 Requirements

You need to install two components:

1. **WinFsp** (filesystem proxy)

   * [https://winfsp.dev](https://winfsp.dev)

2. **SSHFS-Win** (SSH filesystem client)

   * [https://github.com/winfsp/sshfs-win/releases](https://github.com/winfsp/sshfs-win/releases)

---

## 🚀 Setup

1. Install **WinFsp**
2. Install **SSHFS-Win**
3. Restart your system (recommended)

---

## 🔗 Mount a Remote Filesystem

Open **Command Prompt** or **PowerShell** and run:

```bash
net use X: \\sshfs\user@host\path
```

### Example

```bash
net use X: \\sshfs\john@fileserver\home\john
```

* `X:` → drive letter to assign
* `user` → SSH username
* `host` → server hostname or IP
* `path` → remote directory

After running the command, the remote filesystem will appear as a drive in **File Explorer**.

---

## 🔐 Authentication

### Password

* You will be prompted to enter your password if not provided.

### SSH Key

* If SSH keys are configured (e.g., in `~/.ssh`), they will be used automatically.

---

## 🔄 Reconnectable Mount

If you want a more stable connection:

```bash
net use X: \\sshfs.r\user@host\path
```

---

## 🧹 Unmount

To disconnect the drive:

```bash
net use X: /delete
```

---

## ⚠️ Troubleshooting

* Ensure you use **double backslashes (`\\`)**
* Verify SSH access works:

  ```bash
  ssh user@host
  ```
* Check firewall and network access
* Try using the `.r` variant if connection drops

---

## 🟡 Alternative: WSL (Windows Subsystem for Linux)

If you use WSL:

```bash
sudo apt update
sudo apt install sshfs
mkdir ~/mnt
sshfs user@host:/remote/path ~/mnt
```

Access from Windows Explorer:

```
\\wsl$\Ubuntu\home\youruser\mnt
```

---

## 📚 Summary

* `ssh` → remote terminal
* `scp` / `rsync` → file transfer
* `sshfs` → mount remote filesystem as a local drive

---

## ✅ Recommendation

* Use **SSHFS-Win** for simple file access via Explorer
* Use **WSL + sshfs** for development workflows
