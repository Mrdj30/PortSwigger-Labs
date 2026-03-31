# Lab 6 — Username enumeration via account lock

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Use account lockout as an oracle to enumerate a valid username. Then brute-force the password once the lockout expires.

---

## 🪜 Steps

### Step 1 — Try login with a random username and password
Submit a login attempt to capture the request.

> 📸 Screenshot: `./screenshots/step1-login.png`

---

### Step 2 — Intercept and send to Intruder
Capture the `POST /login` request → send to **Intruder**.

> 📸 Screenshot: `./screenshots/step2-intruder.png`

---

### Step 3 — Configure Cluster Bomb attack
- Attack type: **Cluster Bomb**
- Add payload positions on both `username` and `password`

**Payload 1 (username):** PortSwigger username wordlist

**Payload 2 (password):** Null payload — set to generate 5 identical attempts per username
(This sends each username 5 times to trigger lockout on valid accounts)

> 📸 Screenshot: `./screenshots/step3-clusterbomb.png`

---

### Step 4 — Start the attack
Run the attack.

For valid usernames, after 5 attempts you'll see the response:
```
"You have made too many incorrect login attempts. Please try again in 1 minute(s)."
```

Invalid usernames just return the normal error. Sort by **response length** — the locked account stands out.

**Found username: `agent`**

> 📸 Screenshot: `./screenshots/step4-lockout.png`

---

### Step 5 — Login as victim
Wait ~1 minute for the lockout to expire. Then brute-force the password with username fixed as `agent`.

Run a new Sniper attack with the password wordlist. Look for a `302` or a response without the lockout message.

**Found password: `princess`**

Login with:
- Username: `agent`
- Password: `princess`

> 📸 Screenshot: `./screenshots/step5-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Account lockout — while a useful defense — reveals which usernames exist if it only triggers for real accounts. Apply lockout behavior equally for all usernames (even non-existent ones) to prevent this enumeration oracle.
