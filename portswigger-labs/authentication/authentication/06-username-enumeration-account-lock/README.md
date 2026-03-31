# Lab 6 — Username enumeration via account lock

> [← Back to Authentication](../README.md)

---

## 🪜 Steps

### Step 1 — Login with random credentials
![Step 1](./screenshots/image114.png)

---

### Step 2 — Send to Intruder
![Step 2](./screenshots/image92.png)

---

### Step 3 — Cluster Bomb attack
- Payload 1: username wordlist
- Payload 2: null payload × 5 (sends each username 5 times)

Valid accounts get locked → different response.

![Step 3a](./screenshots/image19.png)
![Step 3b](./screenshots/image113.png)

---

### Step 4 — Find locked account
Response with lockout message = valid username.

**Found username: `agent`**

![Step 4](./screenshots/image133.png)

---

### Step 5 — Login as victim
Wait ~1 minute, then brute-force password.

**Password: `princess`**

![Step 5](./screenshots/image81.png)

---

## ✅ Result
- **Username:** `agent`
- **Password:** `princess`
