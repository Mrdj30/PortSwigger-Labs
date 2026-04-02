# 📁 PortSwigger — File Upload Vulnerabilities

> by [Mrdj30](https://github.com/Mrdj30) · Hands-on security research using Burp Suite

---

## 📚 Labs

| # | Lab | Status |
|---|-----|--------|
| 1 | [Remote Code Execution via Avatar Upload](./file-upload-vulnerabilities/01-rce-via-avatar-upload/) | ✅ Solved |
| 2 | [Web Shell Upload via Content-Type Restriction Bypass](./file-upload-vulnerabilities/02-content-type-restriction-bypass/) | ✅ Solved |
| 3 | [Web Shell Upload via Path Traversal](./file-upload-vulnerabilities/03-path-traversal-bypass/) | ✅ Solved |

---

## 🧠 What are File Upload Vulnerabilities?

File upload vulnerabilities occur when a web server allows users to upload files without properly validating the filename, type, contents, or size. Attackers exploit this to upload malicious files — most critically PHP web shells — which can then be executed to achieve Remote Code Execution (RCE).

**Key attack vectors covered:**
- Direct PHP web shell upload (no validation)
- Content-Type header spoofing
- Path traversal in filename (`../exploit.php`)

---

## 🛠️ Tools Used

- **Burp Suite** (Proxy, Repeater)
- **PHP web shell** (`<?php echo file_get_contents('/home/carlos/secret'); ?>`)
- **Browser**

---

*⭐ Star this repo if you find it useful!*
