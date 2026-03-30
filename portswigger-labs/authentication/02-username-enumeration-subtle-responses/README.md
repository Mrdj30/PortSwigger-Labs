# Lab 2 — Username enumeration via subtly different responses

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
The error message is almost identical for all usernames — find the subtle difference to enumerate a valid one.

---

## 🪜 Steps

### Step 1 — Capture login request
Intercept the POST login request in Burp Suite.

> 📸 Add screenshot here

---

### Step 2 — Intruder attack on username
Send to **Intruder**. Set payload on username. Use username wordlist. Run **Sniper attack**.

> 📸 Add screenshot here

---

### Step 3 — Find the subtle difference
In the results, look at the **response length** column. One result will be slightly different (e.g. a missing period at the end of the error message, or 1 character difference).

> 📸 Add screenshot here

---

### Step 4 — Brute-force password
Fix the found username, set payload on password. Run Sniper with password wordlist.

> 📸 Add screenshot here

---

### Step 5 — Login as Carlos
> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Even subtle 1-character differences in responses (e.g. trailing space, different punctuation) can leak enumerable information. Response normalization is critical.
