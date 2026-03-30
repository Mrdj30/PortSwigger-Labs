# Lab 1 — Username enumeration via different responses

> [← Back to Authentication](../README.md)

---

## 🎯 Objective
Enumerate a valid username by looking at different error messages in login responses, then brute-force the password.

---

## 🪜 Steps

### Step 1 — Capture login request
Submit any login attempt and intercept the POST request in Burp.

> 📸 Add screenshot here

---

### Step 2 — Send to Intruder
Send the request to **Intruder**. Set payload position on the username field.

Use **Sniper attack** with PortSwigger's username wordlist.

> 📸 Add screenshot here

---

### Step 3 — Find valid username
When a username is valid, the response message changes from `"Invalid username"` to `"Incorrect password"`.

Sort by **response length** or look for the different message.

> 📸 Add screenshot here

---

### Step 4 — Brute-force the password
Now set the found username as fixed, and brute-force the password field using the password wordlist.

Look for a `302 redirect` or shorter response.

> 📸 Add screenshot here

---

### Step 5 — Login
Use the found credentials to login as Carlos.

> 📸 Add screenshot here

---

## ✅ Result
Lab solved!

---

## 💡 Key Takeaway
Different error messages for invalid username vs wrong password leak which usernames exist. Always return a generic `"Incorrect username or password"` message.
