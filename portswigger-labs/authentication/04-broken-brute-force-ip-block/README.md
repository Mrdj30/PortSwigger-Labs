# Lab 4 — Broken brute-force protection, IP block

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Bypass IP-based brute-force protection by resetting the counter with a valid login every few attempts.

---

## 🪜 Steps

### Step 1 — Capture login request
Intercept the POST login and send to **Intruder**.

> 📸 Add screenshot here

---

### Step 2 — Configure Pitchfork attack
Use **Pitchfork** with two payload positions: username and password.

Build payload lists so that every 3rd request logs in as `wiener:peter` (valid credentials) to reset the IP counter:

**Username list:**
```
wiener
carlos
wiener
carlos
wiener
carlos
...
```

**Password list:**
```
peter
password1
peter
password2
peter
password3
...
```

> 📸 Add screenshot here

---

### Step 3 — Configure Resource Pool
Set max concurrent requests to **1** so requests go in order.

> 📸 Add screenshot here

---

### Step 4 — Start attack and find 302
Look for the request that returns a `302` redirect — that's the correct password.

> 📸 Add screenshot here

---

### Step 5 — Login as Carlos
> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
IP-based rate limiting can be bypassed by resetting the counter with legitimate logins. True brute-force protection must use per-account lockout and CAPTCHA.
