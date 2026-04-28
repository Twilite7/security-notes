# Metasploitable2 -- SQL Injection (DVWA)

## Target
- URL: http://192.168.110.3/dvwa/vulnerabilities/sqli/
- Security level: Low

## What is SQL Injection?
User input is inserted directly into a SQL query without sanitization.
An attacker can break out of the intended query and inject their own SQL.

## Confirming vulnerability
Input a single quote to break query syntax:
Error returned: MySQL syntax error -- confirms injection point.

## Dumping all users
Turns WHERE clause always-true, returns every row in the table.

## Extracting password hashes via UNION injection
UNION appends a second query returning usernames and MD5 hashes.
The # comments out the rest of the original query.

## Cracked hashes
| User | Password |
|---|---|
| admin | password |
| gordonb | abc123 |
| pablo | letmein |
| 1337 | charley |
| smithy | password |

## Takeaway
SQL injection is exploitable from anywhere with browser access.
Always use parameterized queries -- never concatenate user input into SQL.
