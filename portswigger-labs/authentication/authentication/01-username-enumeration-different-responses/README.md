# Lab 1 — Username enumeration via different responses

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Enumerate a valid username via different error messages, then brute-force the password.

---

## 🪜 Steps

### Step 1 — Submit invalid login, investigate response
![Step 1 - Login](./screenshots/image21.png)

---

### Step 2 — Send to Intruder
![Step 2 - Intruder](./screenshots/image102.png)

---

### Step 3 — Sniper attack on username field
Payload: PortSwigger username wordlist. Look for response where message changes to `"Incorrect password"`.

![Step 3 - Attack](./screenshots/image91.png)

**Found username: `ao`**

![Step 3 - Username Found](./screenshots/image29.png)

---

### Step 4 — Brute-force password
Fix `username=ao`, Sniper on password field.

![Step 4 - Password Attack](./screenshots/image137.png)

**Found password: `123456`**

![Step 4 - Password Found](./screenshots/image8.png)

---

### Step 5 — Login and solved
![Step 5 - Solved](./screenshots/image116.png)

---

## ✅ Result
- **Username:** `ao`
- **Password:** `123456`

---

## 💡 Key Takeaway
Different error messages for bad username vs bad password leak which users exist. Always return a single generic error.
