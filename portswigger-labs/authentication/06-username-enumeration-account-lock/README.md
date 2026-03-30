# Lab 6 — Username enumeration via account lock

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Use account lockout behavior as an oracle to enumerate valid usernames, then brute-force the password when the lock expires.

---

## 🪜 Steps

### Step 1 — Capture login request
Intercept the POST login and send to **Intruder**.

> 📸 Add screenshot here

---

### Step 2 — Send each username multiple times
Use **Cluster Bomb** attack or null payload to send the same username 5 times in a row.

If the account gets locked → the username is valid (a lockout error only appears for real accounts).

> 📸 Add screenshot here

---

### Step 3 — Identify the locked account
Sort by response length or look for `"You have made too many incorrect login attempts"` — that username is valid.

> 📸 Add screenshot here

---

### Step 4 — Wait for lockout to expire
Wait ~1 minute for the account to unlock, then brute-force the password.

> 📸 Add screenshot here

---

### Step 5 — Brute-force password
Run Intruder with the valid username fixed, and password wordlist. Look for a response that doesn't say "too many attempts" and returns `302`.

> 📸 Add screenshot here

---

### Step 6 — Login as Carlos
> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Account lockout — while useful — can be abused as an enumeration oracle. Lock all accounts after N attempts (even non-existent ones) to prevent this leak.
