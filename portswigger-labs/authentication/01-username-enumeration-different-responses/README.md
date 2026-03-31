# Lab 1 — Username enumeration via different responses

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Enumerate a valid username by spotting different error messages in login responses, then brute-force the password to login as that user.

---

## 🪜 Steps

### Step 1 — Investigate the login page
Submit an invalid username and password. Observe the error message.

> 📸 Screenshot: `./screenshots/step1-login.png`

---

### Step 2 — Send to Intruder
Intercept the `POST /login` request → send to **Intruder**.

> 📸 Screenshot: `./screenshots/step2-intruder.png`

---

### Step 3 — Enumerate username with Sniper attack
- Attack type: **Sniper**
- Payload position: on the `username` parameter
- Payload: PortSwigger username wordlist

Start the attack. Look for a response where the message changes from `"Invalid username"` to `"Incorrect password"` — that's the valid username.

**Found username: `ao`**

> 📸 Screenshot: `./screenshots/step3-username-found.png`

---

### Step 4 — Brute-force the password
Set the username to `ao` (fixed). Now set payload position on the `password` field.
- Payload: PortSwigger password wordlist

Run another Sniper attack. Look for a **302 redirect** or a different response length.

**Found password: `123456`**

> 📸 Screenshot: `./screenshots/step4-password-found.png`

---

### Step 5 — Login as Carlos
Use the found credentials:
- Username: `ao`
- Password: `123456`

> 📸 Screenshot: `./screenshots/step5-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Different error messages for invalid username vs wrong password leak which usernames exist. Always use a single generic response: `"Incorrect username or password"` for all failed login attempts.
