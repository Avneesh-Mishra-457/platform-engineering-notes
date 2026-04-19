# Linux Day 3 — ps, kill, top

## ps — list processes
```bash
ps aux                  # all processes
ps aux | grep nginx     # find specific process
ps aux | grep kubelet   # check if kubelet running
ps -ef                  # with parent PIDs
```
Columns: USER PID %CPU %MEM COMMAND

## kill — stop a process
```bash
kill 1234       # graceful (SIGTERM)
kill -9 1234    # force (SIGKILL)
killall nginx   # kill by name
```
Always try graceful first. -9 is last resort.

## top — live process monitor
```bash
top     # live view
# q=quit, k=kill, M=sort memory, P=sort CPU
```

## Production use
Node high CPU → top → identify process → ps aux | grep name → investigate

## Quick Revision (Flashcards)
Q: How do you find which process is consuming the most CPU?
A: top, then press P to sort by CPU

Q: What is the difference between kill and kill -9?
A: kill sends SIGTERM (graceful). kill -9 sends SIGKILL (immediate force).

Q: How do you find the PID of nginx?
A: ps aux | grep nginx
