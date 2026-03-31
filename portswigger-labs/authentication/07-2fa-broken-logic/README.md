# Lab 7 — 2FA broken logic

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
The 2FA verification is not properly tied to the logged-in user session. Change the `verify` cookie to target Carlos's account, then brute-force his OTP to gain access.

---

## 🪜 Steps

### Step 1 — Login with your own account
Enter credentials: `wiener:peter`
Intercept the flow in Burp. You'll reach the 2FA page at:
```
GET /login2
```

> 📸 Screenshot: `./screenshots/step1-login.png`

---

### Step 2 — Capture request and send to Repeater
In **HTTP History** → right-click the `GET /login2` request → **Send to Repeater**.

> 📸 Screenshot: `./screenshots/step2-repeater.png`

---

### Step 3 — Change the verify cookie to Carlos
In Repeater, change:
```
Cookie: verify=wiener
```
to:
```
Cookie: verify=carlos
```
Click **Send**.

The server now **generates and sends a 2FA OTP for Carlos's account**. Even though you're logged in as wiener, the server prepares OTP validation for carlos.

> 📸 Screenshot: `./screenshots/step3-verify-carlos.png`

---

### Step 4 — Start login flow again
Login normally (`wiener:peter`). When the 2FA page appears, enter any wrong code.

---

### Step 5 — Intercept POST /login2
Intercept the `POST /login2` request in Burp.

> 📸 Screenshot: `./screenshots/step5-intercept.png`

---

### Step 6 — Send to Intruder and configure Sniper
Send the intercepted request to **Intruder**.

Change the cookie to `verify=carlos`.

Set payload position on the `mfa-code` parameter:
- Attack type: **Sniper**
- Payload type: **Brute force**
- Min/Max length: **4 digits** (0000–9999)

> 📸 Screenshot: `./screenshots/step6-intruder.png`

---

### Step 7 — Start brute force
Run the attack. Look for **Status code = 302**.

**Found OTP: `0377`**

> 📸 Screenshot: `./screenshots/step7-otp-found.png`

---

### Step 8 — Enter OTP in browser
Enter `0377` on the 2FA page (with `verify=carlos` cookie active).

> 📸 Screenshot: `./screenshots/step8-solved.png`

---

## ✅ Result
Lab solved! Logged in as Carlos.

---

## 💡 Key Takeaway
2FA codes must be cryptographically bound to the specific user session. If the server derives the target account from an attacker-controlled cookie, the entire 2FA mechanism is bypassable.
