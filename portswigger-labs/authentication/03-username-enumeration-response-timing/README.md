# Lab 3 — Username enumeration via response timing

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Enumerate valid usernames by measuring response time differences — valid usernames take longer to process (password hashing happens only for real accounts). Then brute-force the password.

---

## 🪜 Steps

### Step 1 — Capture login request
Intercept the `POST /login` request → send to **Intruder**.

> 📸 Screenshot: `./screenshots/step1-capture.png`

---

### Step 2 — Add X-Forwarded-For to bypass rate limiting
Add the header `X-Forwarded-For: 1` to your request.
Make this a **payload position** too — change the value each request to spoof a different IP.

---

### Step 3 — Configure Pitchfork attack
- Attack type: **Pitchfork**
- Position 1: `X-Forwarded-For` value (incremental numbers: 1, 2, 3...)
- Position 2: `username` (PortSwigger username wordlist)

Use a **very long password** (100+ characters) to exaggerate the timing difference for valid usernames.

> 📸 Screenshot: `./screenshots/step3-pitchfork.png`

---

### Step 4 — Analyze response times
Sort results by **Response received** time column.

One username will take noticeably longer — that's the valid one (the server is actually hashing the long password for it).

**Found username: `agenda`**

> 📸 Screenshot: `./screenshots/step4-timing.png`

---

### Step 5 — Brute-force the password
Fix username as `agenda`. Run another Pitchfork with `X-Forwarded-For` incrementing + password wordlist.

Look for a `302` redirect.

**Found password: `baseball`**

> 📸 Screenshot: `./screenshots/step5-password.png`

---

### Step 6 — Login
Credentials:
- Username: `agenda`
- Password: `baseball`

> 📸 Screenshot: `./screenshots/step6-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Timing side-channels leak valid usernames even when responses look identical. Use constant-time password comparison regardless of whether the username exists, to prevent this attack.
