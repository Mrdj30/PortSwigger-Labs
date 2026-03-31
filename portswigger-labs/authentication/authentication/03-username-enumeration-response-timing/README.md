# Lab 3 — Username enumeration via response timing

> [← Back to Authentication](../README.md)

---

## 🪜 Steps

### Step 1 — Capture login request, send to Intruder
![Step 1](./screenshots/image4.png)
![Step 1b](./screenshots/image43.png)

---

### Step 2 — Add X-Forwarded-For header (bypass rate limit)
Add: `X-Forwarded-For: 1` as a payload position.

---

### Step 3 — Pitchfork attack: X-Forwarded-For + username
Use a very long password (100+ chars) to amplify timing differences.

![Step 3 - Config](./screenshots/image110.png)

---

### Step 4 — Analyze response times
Sort by response time. One username takes noticeably longer.

**Found username: `agenda`**

![Step 4 - Timing](./screenshots/image126.png)

---

### Step 5 — Brute-force password
![Step 5 - Password Attack](./screenshots/image54.png)
![Step 5 - Found](./screenshots/image69.png)

**Found password: `baseball`**

---

### Step 6 — Login and solved
- **Username:** `agenda`
- **Password:** `baseball`

![Step 6 - Solved](./screenshots/image117.png)

---

## ✅ Result
- **Username:** `agenda`
- **Password:** `baseball`
