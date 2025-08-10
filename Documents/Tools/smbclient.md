```
# List all available shares anonymously
smbclient -L //<TARGET_IP> -U Anonymous

# Connect to a specific share anonymously
smbclient //<TARGET_IP>/profiles -U Anonymous
```