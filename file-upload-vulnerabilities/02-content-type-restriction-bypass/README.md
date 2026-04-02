# Lab 2 — Web Shell Upload via Content-Type Restriction Bypass

> [← Back to File Upload Vulnerabilities](../README.md)

---

## 🎯 Objective
The server validates file type using the `Content-Type` header only — not the actual file content. Spoof it to upload a PHP web shell.

---

## 🪜 Steps

### Step 1 — Login
Credentials: `wiener:peter`

Upload a legitimate image first to observe normal behaviour.

![Step 1a](./screenshots/image22.png)
![Step 1b](./screenshots/image21.png)
![Step 1c](./screenshots/image8.png)

---

### Step 2 — Capture upload request in Burp
Go to **Burp → Proxy → HTTP history** → find `POST /my-account/avatar`.

![Step 2](./screenshots/image19.png)

---

### Step 3 — Try uploading PHP directly — blocked
Upload `exploit.php` with `Content-Type: application/x-php` → server rejects it.

![Step 3a](./screenshots/image15.png)
![Step 3b](./screenshots/image20.png)

---

### Step 4 — Spoof Content-Type to bypass
Send the upload request to **Repeater**. Change:
```
Content-Disposition: form-data; name="avatar"; filename="exploit.php"
Content-Type: image/jpeg      ← spoof as image
```

The server trusts the `Content-Type` header and accepts the file.

![Step 4a](./screenshots/image11.png)
![Step 4b](./screenshots/image25.png)

---

### Step 5 — Execute the payload
Request the uploaded file:
```
GET /files/avatars/exploit.php
```

![Step 5](./screenshots/image24.png)

---

### Step 6 — Submit solution
Copy secret → Submit → Lab solved ✅

![Step 6a](./screenshots/image6.png)
![Step 6b](./screenshots/image17.png)

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Never trust the `Content-Type` header for file validation — it is fully controlled by the client and can be changed in Burp in seconds. Always validate the actual file content (magic bytes) server-side.
