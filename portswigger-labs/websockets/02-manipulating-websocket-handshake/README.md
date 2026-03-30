# Lab 2 — Manipulating the WebSocket handshake to exploit vulnerabilities

> [← Back to WebSockets](../README.md)

---

## 🎯 Objective
Bypass an IP ban by manipulating the WebSocket handshake headers, then exploit XSS via an obfuscated payload.

---

## 🪜 Steps

### Step 1 — Open live chat and send XSS
Open the chat and send a basic XSS payload. The server detects it and bans your IP.

> 📸 Add screenshot here

---

### Step 2 — Attempt to reconnect
Try reconnecting — you are blocked.

> 📸 Add screenshot here

---

### Step 3 — Bypass the IP ban
Intercept the WebSocket **upgrade/handshake** request in Burp Proxy.
Add the header:
```
X-Forwarded-For: 1.1.1.1
```
This spoofs your IP and bypasses the ban.

> 📸 Add screenshot here

---

### Step 4 — Send obfuscated XSS payload
Send a modified XSS payload that evades the filter:
```
<img src=x oNeRrOr=alert`1`>
```
(Obfuscate the event handler casing to bypass detection)

> 📸 Add screenshot here

---

### Step 5 — Successful exploitation
The alert fires — XSS confirmed.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
IP-based bans can be bypassed with `X-Forwarded-For` headers. WAF/filter bypass often works by obfuscating casing or encoding. Defense must be layered — not just IP-based.
