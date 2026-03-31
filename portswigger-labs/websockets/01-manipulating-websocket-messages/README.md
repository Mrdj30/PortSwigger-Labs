# Lab 1 — Manipulating WebSocket messages to exploit vulnerabilities

> [← Back to WebSockets](../README.md)

---

## 🎯 Objective
Inject an XSS payload through a WebSocket message to execute JavaScript in the victim's browser.

---

## 🪜 Steps

### Step 1 — Open Live Chat
Open the lab. Start Burp proxy. When the page loads, click **Live Chat**.

> 📸 Screenshot: `./screenshots/step1-livechat.png`

---

### Step 2 — Send a message and capture it
Type `Hello` in the chat and send it. The WebSocket message is captured in Burp Suite.

> 📸 Screenshot: `./screenshots/step2-hello.png`

---

### Step 3 — View in WebSockets history
Go to **Burp → Proxy → WebSockets history**.

You'll see the message:
```json
{"message":"Hello"}
```

> 📸 Screenshot: `./screenshots/step3-wshistory.png`

---

### Step 4 — Test with `<` character
Go back to Live Chat and send the character `<`.

In Burp WebSockets history, you'll see:
```json
{"message":"&lt;"}
```
This shows the app encodes `<` — but let's check if we can bypass via Burp Intercept.

> 📸 Screenshot: `./screenshots/step4-ltchar.png`

---

### Step 5 — Intercept and inject XSS
Enable **Intercept** in Burp. Send any test message in Live Chat.

When the request is captured, modify it from:
```json
{"message":"test"}
```
to:
```json
{"message":"<img src=1 onerror='alert(1)'>"}
```

Forward the request.

> 📸 Screenshot: `./screenshots/step5-payload.png`

---

### Step 6 — Alert fires
The XSS executes in the browser — `alert(1)` pops up. Lab solved!

> 📸 Screenshot: `./screenshots/step6-alert.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
WebSocket messages are often trusted without server-side sanitization. Always treat WebSocket input the same as HTTP form input — validate and encode on both client and server.
