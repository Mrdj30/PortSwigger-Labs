# Lab 5 — Password reset broken logic

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Exploit broken password reset logic to reset Carlos's password and login to his account.

---

## 🪜 Steps

### Step 1 — Trigger password reset for yourself
Use the "Forgot password" feature for `wiener`. Check your email for the reset link.

> 📸 Add screenshot here

---

### Step 2 — Intercept the reset request
Click the reset link and intercept the POST request that submits the new password.

> 📸 Add screenshot here

---

### Step 3 — Inspect the parameters
Look at the POST body. You'll see something like:
```
temp-forgot-password-token=TOKEN&username=wiener&new-password-1=test&new-password-2=test
```

> 📸 Add screenshot here

---

### Step 4 — Change username to carlos
In Burp Repeater, change `username=wiener` to `username=carlos` and forward the request.

> 📸 Add screenshot here

---

### Step 5 — Login as Carlos
Use `carlos` with the new password you just set.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Password reset tokens must be tied to a specific user server-side. If the username is trusted from the POST body instead of the token, attackers can reset any account's password.
