# Lab 8 — Password brute-force via password change

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Exploit the password change functionality to brute-force Carlos's current password. When the new passwords don't match, the server reveals a different error message for correct vs incorrect current passwords.

---

## 🪜 Steps

### Step 1 — Login with your account
Login using: `wiener:peter`

> 📸 Screenshot: `./screenshots/step1-login.png`

---

### Step 2 — Go to password change and capture request
Navigate to the password change page. Submit:
- Current password: `wrongvalue`
- New password: `123`
- Confirm password: `abc` *(deliberately different)*

Capture this request in **Burp Suite**.

> 📸 Screenshot: `./screenshots/step2-capture.png`

---

### Step 3 — Send to Intruder
Send the `POST /my-account/change-password` request to **Intruder**.

Modify the request body:
```
username=carlos&current-password=§incorrect-password§&new-password-1=123&new-password-2=abc
```

- Attack type: **Sniper**
- Payload position: `current-password`
- Payload: PortSwigger password wordlist

> 📸 Screenshot: `./screenshots/step3-intruder.png`

---

### Step 4 — Add Grep Match
Under **Grep - Match**, add the string:
```
New passwords do not match
```

When the current password is **correct**, the server tries to change it and returns `"New passwords do not match"` (because `123 ≠ abc`).

When the current password is **wrong**, it returns a different message.

This is the oracle.

> 📸 Screenshot: `./screenshots/step4-grep.png`

---

### Step 5 — Launch attack and find Carlos's password
Start the attack. Sort by the **Grep match** column.

The request that returns `"New passwords do not match"` = correct current password for Carlos.

**Found password: `thunder`**

> 📸 Screenshot: `./screenshots/step5-password-found.png`

---

### Step 6 — Login as Carlos
Use:
- Username: `carlos`
- Password: `thunder`

> 📸 Screenshot: `./screenshots/step6-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Password change forms can be exploited as brute-force oracles if they return different error messages depending on whether the current password is correct. All password-related error messages should be generic and identical.
