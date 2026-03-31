# Lab 2 — Username enumeration via subtly different responses

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
The error messages look almost identical for all inputs — find the subtle 1-character difference that reveals a valid username.

---

## 🪜 Steps

### Step 1 — Investigate the login page
Submit an invalid username and password. Note the error message.

> 📸 Screenshot: `./screenshots/step1-login.png`

---

### Step 2 — Send to Intruder
Intercept the `POST /login` request → send to **Intruder**.

> 📸 Screenshot: `./screenshots/step2-intruder.png`

---

### Step 3 — Set up Grep-Extract
Under **Grep - Extract** in Intruder settings, click **Add**.
Scroll through the response → highlight the error message `Invalid username or password.`

This lets Intruder extract and compare the exact error text for each response.

> 📸 Screenshot: `./screenshots/step3-grep-extract.png`

---

### Step 4 — Run Sniper attack on username
- Attack type: **Sniper**
- Payload position: `username`
- Payload: PortSwigger username wordlist

Start the attack. Sort by the extracted column.

One response will be subtly different — for example, missing a trailing period: `"Invalid username or password"` vs `"Invalid username or password."` — that's your valid username.

**Found username: `ads`**

> 📸 Screenshot: `./screenshots/step4-username-found.png`

---

### Step 5 — Brute-force the password
Fix username as `ads`. Set payload position on `password`. Use password wordlist.

Look for `302` redirect.

**Found password: `123qwe`**

> 📸 Screenshot: `./screenshots/step5-password-found.png`

---

### Step 6 — Login
Use the credentials:
- Username: `ads`
- Password: `123qwe`

> 📸 Screenshot: `./screenshots/step6-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Even a 1-character difference in error messages (like a missing period) is enough to enumerate valid usernames. Response normalization — returning exactly identical text and length for all failed logins — is critical.
