# Lab 3 — Exploiting origin server normalization for web cache deception

> [← Back to Web Cache Deception](../README.md)

---

## 🎯 Objective
The origin server normalizes encoded dot-segments. Exploit this to cache Carlos's account page under `/resources/` and steal his API key.

---

## 🪜 Steps

### Step 1 — Login (wiener:peter)
![Step 1 - Login](./screenshots/image37.png)

---

### Step 2 — Intercept and send to Repeater
![Step 2 - Repeater](./screenshots/image101.png)

---

### Step 3 — Test path handling
- `/my-account/abc` → 404
![Step 3a](./screenshots/image23.png)
- `/my-accountabc` → 404
![Step 3b](./screenshots/image134.png)

---

### Step 4 — Find delimiter via Intruder Sniper
Sniper attack, uncheck URL-encode. Only `?` returns **200 OK**.

![Step 4 - Intruder](./screenshots/image80.png)
![Step 4 - Result](./screenshots/image96.png)

---

### Step 5 — Test URL normalization on origin
Try: `GET /aaa/..%2fmy-account` → **200 OK** + API key visible.

Origin resolves the encoded dot-segment. Normalization confirmed.

![Step 5 - Normalization](./screenshots/image135.png)
![Step 5 - API Key](./screenshots/image93.png)

---

### Step 6 — Identify cache rules (/resources/)
- 1st request → `X-Cache: miss`
![Step 6 - Miss](./screenshots/image108.png)
- 2nd request → `X-Cache: hit` ✅
![Step 6 - Hit](./screenshots/image112.png)
![Step 6 - Miss 2](./screenshots/image99.png)
![Step 6 - Hit 2](./screenshots/image128.png)

---

### Step 7 — Exploit: combine cache rule + normalization
Try: `GET /resources/..%2fmy-account`
- 1st → miss
![Step 7 - Miss](./screenshots/image24.png)
- 2nd → **hit** ✅
![Step 7 - Hit](./screenshots/image27.png)

---

### Step 8 — Deliver exploit to victim
![Step 8 - Exploit Server](./screenshots/image123.png)
![Step 8 - After Deliver](./screenshots/image106.png)

---

### Step 9 — Get Carlos's API key
Request `GET /resources/..%2fmy-account?wcd` — cached response has Carlos's API key.

![Step 9 - API Key](./screenshots/image63.png)
![Step 9 - API Key 2](./screenshots/image61.png)
![Step 9 - Solved](./screenshots/image73.png)

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
When the origin normalizes encoded dot-segments but the cache does not, attackers craft URLs the cache treats as static but the origin resolves to sensitive pages.
