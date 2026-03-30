# Lab 3 — Username enumeration via response timing

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Enumerate valid usernames by measuring response time differences — valid usernames take longer to process.

---

## 🪜 Steps

### Step 1 — Capture login request
Intercept POST login request.

> 📸 Add screenshot here

---

### Step 2 — Add X-Forwarded-For to bypass rate limiting
Add the header `X-Forwarded-For: §1§` so each request appears from a different IP. Set this as a payload position too.

> 📸 Add screenshot here

---

### Step 3 — Configure Pitchfork attack
Use **Pitchfork** attack with two payload positions:
- Position 1: `X-Forwarded-For` value (incremental numbers: 1, 2, 3...)
- Position 2: username (username wordlist)

Use a **very long password** (100+ chars) to amplify timing differences.

> 📸 Add screenshot here

---

### Step 4 — Analyze response times
Sort results by **response received** time. Valid usernames will have noticeably longer response times.

> 📸 Add screenshot here

---

### Step 5 — Brute-force password
Fix the found username, repeat Pitchfork attack for password. Look for `302` redirect.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Timing side-channels can leak valid usernames even when responses look identical. Use constant-time comparison for passwords regardless of whether the username exists.
