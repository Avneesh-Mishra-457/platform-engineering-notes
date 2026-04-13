# Linux Basics — Day 1

## Filesystem Structure
- `/etc/` — config files (settings for everything)
- `/var/log/` — logs and variable data
- `/usr/bin/` — user programs and binaries
- `/home/` — personal folders for users
- `/tmp/` — temporary files (deleted on reboot)
- `/proc/` — virtual fs for running processes
- `/bin/` — essential binaries (ls, cp, mv)

Mnemonic: **Every Variable User Homes Temporary Processes in Bins**

## Essential Commands
| Command | Use |
|---|---|
| `pwd` | current directory |
| `ls -la` | list all files with permissions |
| `cd /path` | navigate |
| `cat file` | print file contents |
| `grep "term" file` | search in file |
| `find / -name "*.conf"` | find files |
| `chmod 755 script.sh` | set permissions |
| `ps aux` | list processes |
| `tail -f logfile` | watch log live |
| `cmd1 \| cmd2` | pipe output |

## Permissions
`-rwxr-xr--` → owner / group / other

| Number | Permissions | Meaning |
|---|---|---|
| 7 | rwx | Read + Write + Execute |
| 6 | rw- | Read + Write |
| 5 | r-x | Read + Execute |
| 4 | r-- | Read only |
| 0 | --- | No permissions |

`chmod 755` = owner full (7), group r+x (5), others r+x (5)

First character: `-` = file, `d` = directory, `l` = symlink

## Quick Revision (Flashcards)
Q: What is /etc used for?
A: Configuration files

Q: What is /proc?
A: Virtual filesystem — shows running processes, not real files

Q: What does chmod 755 mean?
A: Owner has full access (rwx), group and others can read and execute

Q: How do you watch a log file in real time?
A: tail -f /path/to/logfile

Q: How do you find all .conf files on the system?
A: find / -name "*.conf"
