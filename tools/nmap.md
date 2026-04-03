# Nmap

Network mapper. Used for host discovery, port scanning, service detection, and OS fingerprinting.

## Port States

| State | Meaning |
|---|---|
| Open | A service is actively listening |
| Closed | Port reachable but nothing running |
| Filtered | Firewall blocking the probe |

## Essential Flags

| Flag | Purpose |
|---|---|
| `-sn` | Ping scan (host discovery only) |
| `-sV` | Service version detection |
| `-O` | OS fingerprinting |
| `-p-` | Scan all 65535 ports |
| `-oA <name>` | Save output in all formats |

## Common Scans
```bash
# Discover live hosts on a subnet
nmap -sn 10.0.2.0/24

# Basic port + version scan
nmap -sV <target>

# Full scan with OS detection
sudo nmap -sV -O <target>
```

## Key Takeaways

- NAT and firewalls distort OS fingerprint results
- `-sV` costs more time but gives version info
- Always save output with `-oA` on real engagements
