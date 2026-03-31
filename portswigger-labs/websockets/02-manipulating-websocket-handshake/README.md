# Lab 2 — Manipulating the WebSocket handshake to exploit vulnerabilities

> [← Back to WebSockets](../README.md)

---

## 🎯 Objective
Bypass an IP ban triggered by a WAF, then exploit XSS via an obfuscated payload through WebSocket messages.

---

## 🪜 Steps

### Step 1 — Open Live Chat and send a message
Open the lab → click **Live Chat** → send: `hello`

> 📸 Screenshot: `./screenshots/step1-hello.png`

---

### Step 2 — Capture WebSocket message in Burp
Go to **Burp → Proxy → WebSockets history**.
You'll see:
```json
{"message":"hello"}
```

> 📸 Screenshot: `./screenshots/step2-ws-history.png`

---

### Step 3 — Send to Repeater and test XSS
Right-click the WebSocket message → **Send to Repeater**.

In Repeater, modify the message to:
```json
{"message":"<img src=1 onerror='alert(1)'>"}
```
Click Send.

**Server response:**
```json
{"error":"Attack detected: Event handler"}
```
The WAF blocks the payload and **bans your IP**.

> 📸 Screenshot: `./screenshots/step3-detected.png`

---

### Step 4 — Try to reconnect — fails
Click **Reconnect** in Repeater. Connection fails due to IP ban.

> 📸 Screenshot: `./screenshots/step4-reconnect-fail.png`

---

### Step 5 — Bypass IP ban via handshake header
Edit the WebSocket **handshake** (upgrade) request. Add the header:
```
X-Forwarded-For: 1.1.1.1
```
This spoofs your IP and bypasses the ban. Reconnect succeeds.

> 📸 Screenshot: `./screenshots/step5-xforwarded.png`

---

### Step 6 — Send obfuscated XSS payload
Now send an obfuscated version of the payload that bypasses the WAF filter:
```json
{"message":"<img src=1 oNeRrOr=alert`1`>"}
```
Obfuscation used: mixed case on the event handler (`oNeRrOr`) and backtick syntax for `alert`.

> 📸 Screenshot: `./screenshots/step6-obfuscated.png`

---

### Step 7 — Alert fires — XSS confirmed
The `alert(1)` executes in the browser. Lab solved!

> 📸 Screenshot: `./screenshots/step7-alert.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
IP-based bans can be bypassed with `X-Forwarded-For` headers. WAF filters based on keyword matching can be bypassed by obfuscating case or using alternate syntax. Defense must be layered — not just IP or pattern based.
