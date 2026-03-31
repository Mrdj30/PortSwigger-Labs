# Lab 5 — Password reset broken logic

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
The password reset mechanism trusts the `username` from the POST body instead of binding it to the reset token server-side. Exploit this to reset Carlos's password and login to his account.

---

## 🪜 Steps

### Step 1 — Trigger password reset for your account
Go to: **Forgot password?**
Enter: `wiener` → Click **Email client** → Open the reset link.

> 📸 Screenshot: `./screenshots/step1-forgot.png`

---

### Step 2 — Capture the reset request
Enter a new password for your account and click Submit.

Go to **Burp → Proxy → HTTP history**.
Find the request:
```
POST /forgot-password?temp-forgot-password-token=XXXX
```

> 📸 Screenshot: `./screenshots/step2-reset-request.png`

---

### Step 3 — Send to Repeater
Right-click → **Send to Repeater**.

---

### Step 4 — Break the logic
In Repeater, look at the POST body:
```
temp-forgot-password-token=XXXX&username=wiener&new-password-1=test&new-password-2=test
```

Make two changes:
1. Clear the token: `temp-forgot-password-token=`
2. Change username: `username=carlos`

> 📸 Screenshot: `./screenshots/step4-modify.png`

---

### Step 5 — Send the request
Click **Send**.

If response is **200 OK** → the attack worked. Carlos's password is now set to whatever you put in `new-password-1`.

> 📸 Screenshot: `./screenshots/step5-200ok.png`

---

### Step 6 — Login as Carlos
Use:
- Username: `carlos`
- Password: *(whatever you set in step 4)*

> 📸 Screenshot: `./screenshots/step6-solved.png`

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Password reset tokens must be cryptographically bound to a specific user server-side. Never trust the username from the POST body — always derive it from the validated token.
