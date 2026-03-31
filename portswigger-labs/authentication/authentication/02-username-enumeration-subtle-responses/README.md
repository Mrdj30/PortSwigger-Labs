# Lab 2 — Username enumeration via subtly different responses

> [← Back to Authentication](../README.md)

---

## 🪜 Steps

### Step 1 — Submit invalid login
![Step 1](./screenshots/image104.png)

---

### Step 2 — Send to Intruder
![Step 2](./screenshots/image31.png)

---

### Step 3 — Add Grep-Extract for error message
Under **Grep - Extract → Add** → highlight `Invalid username or password.`

One response will have a subtle difference (e.g. missing trailing period).

![Step 3 - Grep Extract](./screenshots/image84.png)

**Found username: `ads`**

![Step 3 - Found](./screenshots/image60.png)

---

### Step 4 — Brute-force password
![Step 4](./screenshots/image55.png)

**Found password: `123qwe`**

![Step 4 - Password](./screenshots/image10.png)

---

### Step 5 — Login and solved
![Step 5 - Solved](./screenshots/image136.png)

---

## ✅ Result
- **Username:** `ads`
- **Password:** `123qwe`
