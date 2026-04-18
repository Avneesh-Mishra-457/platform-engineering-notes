# Linux Day 2 — grep, find, permissions

## grep — Search inside text and command output
```bash
grep "error" app.log
grep -i "error" app.log
grep -n "error" app.log
grep -r "error" /var/log/
grep -v "error" app.log
ps aux | grep nginx
kubectl logs mypod | grep ERROR
kubectl get pods | grep nginx
```

## find — Locate files on filesystem
```bash
find / -name "nginx.conf"
find /etc -name "*.conf"
find /var -type f -name "*.log"
find /var/log -mtime -1
find /tmp -name "*.tmp" -delete
find /var/log -name "*.log" | xargs grep "error"
```

## grep vs find
| Tool | Use for |
|---|---|
| grep | Searching inside text, logs, command output |
| find | Locating files on filesystem |
| grep + pipe | Filtering kubectl, docker, ps output |
| find + xargs + grep | Search inside many files at once |

## Permissions
-rwxr-xr--
owner group others

| Octal | Permissions |
|---|---|
| 7 | rwx full |
| 6 | rw- read+write |
| 5 | r-x read+execute |
| 4 | r-- read only |
| 0 | --- none |

```bash
chmod 755 script.sh
chmod 644 config.yml
chmod 600 secret.key
chown user:group file
chown -R user /app/
```

## Quick Revision (Flashcards)
Q: How do you search for errors in all log files recursively?
A: grep -r "error" /var/log/

Q: How do you filter kubectl output to find a specific pod?
A: kubectl get pods | grep podname

Q: Can find be used with kubectl output?
A: No. find only works on filesystem. Use grep for command output.

Q: What does chmod 600 mean?
A: Owner read+write only. No access for group or others. Used for secrets.

Q: How do you find all .conf files on the system?
A: find / -name "*.conf"
