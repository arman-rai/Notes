```bash
john --show <hashfile>
```

### Crack `/etc/shadow`:

```bash
unshadow /etc/passwd /etc/shadow > shadow.hash
john shadow.hash
```

| Option              | Description                 |
| ------------------- | --------------------------- |
| `--format=<type>`   | Manually set hash type      |
| `--wordlist=<file>` | Use wordlist                |
| `--rules`           | Enable wordlist mangling    |
| `--incremental`     | Bruteforce mode             |
| `--show`            | Show cracked passwords      |
| `--restore`         | Resume session              |
| `--session=<name>`  | Save named cracking session |
| `--pot=<file>`      | Custom potfile location     |
