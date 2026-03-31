# Lab 4 — Exploiting cache server normalization for web cache deception

> [← Back to Web Cache Deception](../README.md)

---

## 🎯 Objective
The **cache server** (not the origin) normalizes encoded dot-segments. Exploit this to poison the cache with Carlos's account data.

---

## 🪜 Steps

### Step 1 — Login (wiener:peter)
![Step 1 - Login](./screenshots/image65.png)
![Step 1 - Login 2](./screenshots/image122.png)

---

### Step 2 — Send to Repeater
![Step 2 - Repeater](./screenshots/image94.png)

---

### Step 3 — Test path handling (404s)
![Step 3a](./screenshots/image105.png)
![Step 3b](./screenshots/image78.png)

---

### Step 4 — Find delimiter via Intruder
`?` returns **200 OK**.

![Step 4 - Intruder](./screenshots/image35.png)
![Step 4 - Result](./screenshots/image45.png)

---

### Step 5 — Confirm delimiter path
`GET /my-account?abc.js` → **200 OK**

![Step 5 - Delimiter OK](./screenshots/image83.png)

---

### Step 6 — Test normalization (origin returns 404)
`GET /aaa/..%2fmy-account` → **404** — origin does NOT normalize. Cache does.

![Step 6 - 404](./screenshots/image66.png)

---

### Step 7 — Cache stores /resources/ paths
- 1st → miss
![Step 7 - Miss](./screenshots/image111.png)
- 2nd → hit ✅
![Step 7 - Hit](./screenshots/image26.png)

---

### Step 8 — Add encoded dot-segment after /resources
`GET /resources/..%2fmy-account`
- 1st → miss
![Step 8 - Miss](./screenshots/image3.png)
- 2nd → **hit** ✅
![Step 8 - Hit](./screenshots/image49.png)

---

### Step 9 — Craft the exploit path
`/my-account?%2f%2e%2e%2fresources`

![Step 9 - Craft](./screenshots/image36.png)

---

### Step 10 — Deliver exploit to victim
![Step 10 - Exploit](./screenshots/image125.png)
![Step 10 - After](./screenshots/image85.png)

---

### Step 11 — Get Carlos's API key
![Step 11 - API Key](./screenshots/image67.png)
![Step 11 - API Key 2](./screenshots/image53.png)
![Step 11 - Solved](./screenshots/image118.png)

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Cache-side normalization allows attackers to poison the cache with sensitive content under static-looking paths.
