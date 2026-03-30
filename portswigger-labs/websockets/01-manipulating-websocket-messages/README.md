# Lab 1 — Manipulating WebSocket messages to exploit vulnerabilities

> [← Back to WebSockets](../README.md)

---

## 🎯 Objective
Exploit a live chat WebSocket connection by injecting an XSS payload via a manipulated message.

---

## 🪜 Steps

### Step 1 — Open the live chat
Navigate to the live chat feature on the target site.

> 📸 Add screenshot here

---

### Step 2 — Capture the WebSocket message
In Burp Suite, go to **Proxy → WebSockets history**.
Send a chat message and capture the WebSocket frame.

> 📸 Add screenshot here

---

### Step 3 — Send to Repeater
Right-click the captured WebSocket message → **Send to Repeater**.

> 📸 Add screenshot here

---

### Step 4 — Inject XSS payload
In Repeater, modify the message content to:
```
<img src=x onerror=alert(1)>
```
Send the message.

> 📸 Add screenshot here

---

### Step 5 — Confirm XSS execution
The alert fires in the browser, confirming the server reflects the message without sanitization.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
WebSocket messages are often trusted without sanitization. Always treat WebSocket input the same as HTTP input — validate and encode on both client and server.
