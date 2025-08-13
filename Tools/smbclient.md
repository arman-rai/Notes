```
# List all available shares anonymously
smbclient -L //<TARGET_IP> -U Anonymous

# Connect to a specific share anonymously
smbclient //<TARGET_IP>/profiles -U Anonymous

# Specify workgroup (when default doesn't work)
smbclient //<TARGET_IP>/share -U user -W WORKGROUP

# Use specific port (non-standard SMB)
smbclient //<TARGET_IP>:445/share -U user

# Debug mode (verbose output)
smbclient -d3 //<TARGET_IP>/share -U user

# Use NTLM authentication
smbclient //<TARGET_IP>/share -U user --authentication-ntlm

# Kerberos authentication (domain environments)
smbclient -k //<TARGET_IP>/share
```
