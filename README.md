<div align="center">

# 🛡️ PortSwigger Web Security Academy — Lab Writeups

**Hands-on security research using Burp Suite**

[![Labs Solved](https://img.shields.io/badge/Labs%20Solved-32-brightgreen?style=for-the-badge&logo=checkmarx)](https://github.com/Mrdj30/portswigger-labs)
[![Categories](https://img.shields.io/badge/Categories-5-blue?style=for-the-badge&logo=bookstack)](https://github.com/Mrdj30/portswigger-labs)
[![Platform](https://img.shields.io/badge/Platform-PortSwigger-orange?style=for-the-badge&logo=burpsuite)](https://portswigger.net/web-security)
[![Tool](https://img.shields.io/badge/Tool-Burp%20Suite-red?style=for-the-badge)](https://portswigger.net/burp)

> Detailed walkthroughs of PortSwigger Web Security Academy labs, covering real-world web vulnerabilities with step-by-step exploitation techniques.

[🚀 Get Started](#-learning-path) · [📚 Browse Labs](#-lab-categories) · [🛠️ Tools](#%EF%B8%8F-tools--prerequisites)

</div>

---

## 📋 Table of Contents

- [📊 Progress Dashboard](#-progress-dashboard)
- [📚 Lab Categories](#-lab-categories)
  - [🟡 Authentication](#-authentication--14-labs)
  - [📁 File Upload Vulnerabilities](#-file-upload-vulnerabilities--6-labs)
  - [🔵 SSRF](#-server-side-request-forgery-ssrf--5-labs)
  - [🔴 Web Cache Deception](#-web-cache-deception--4-labs)
  - [🟠 WebSockets](#-websockets--3-labs)
- [🎓 Learning Path](#-learning-path)
- [📖 How to Use](#-how-to-use)
- [🛠️ Tools & Prerequisites](#%EF%B8%8F-tools--prerequisites)
- [📬 Contact](#-contact)

---

## 📊 Progress Dashboard

| Category | Labs Solved | Difficulty | Status |
|----------|:-----------:|:----------:|:------:|
| 🟡 Authentication | 14 / 14 | 🟢🟡🔴 Easy → Hard | ✅ Complete |
| 📁 File Upload Vulnerabilities | 6 / 6 | 🟢🟡🔴 Easy → Hard | ✅ Complete |
| 🔵 Server-Side Request Forgery | 5 / 5 | 🟢🟡 Easy → Medium | ✅ Complete |
| 🔴 Web Cache Deception | 4 / 4 | 🟡🔴 Medium → Hard | ✅ Complete |
| 🟠 WebSockets | 3 / 3 | 🟢🟡🔴 Easy → Hard | ✅ Complete |
| **Total** | **32 / 32** | | 🏆 **All Solved** |

---

## 📚 Lab Categories

### 🟡 Authentication — [14 labs](./authentication/)

> Bypass login mechanisms, brute-force credentials, and hijack accounts through enumeration, logic flaws, and rate-limiting bypasses.

| # | Lab | Difficulty | Status |
|---|-----|:----------:|:------:|
| 1 | [Username enumeration via different responses](./authentication/01-username-enumeration-different-responses/) | 🟢 Easy | ✅ |
| 2 | [Username enumeration via subtly different responses](./authentication/02-username-enumeration-subtle-responses/) | 🟢 Easy | ✅ |
| 3 | [Username enumeration via response timing](./authentication/03-username-enumeration-response-timing/) | 🟡 Medium | ✅ |
| 4 | [Broken brute-force protection, IP block](./authentication/04-broken-brute-force-ip-block/) | 🟡 Medium | ✅ |
| 5 | [Password reset broken logic](./authentication/05-password-reset-broken-logic/) | 🟢 Easy | ✅ |
| 6 | [Username enumeration via account lock](./authentication/06-username-enumeration-account-lock/) | 🟡 Medium | ✅ |
| 7 | [2FA broken logic](./authentication/07-2fa-broken-logic/) | 🟡 Medium | ✅ |
| 8 | [Password brute-force via password change](./authentication/08-password-brute-force-via-password-change/) | 🟡 Medium | ✅ |
| 9 | [Username enumeration via account lock (v2)](./authentication/09-username-enumeration-account-lock-v2/) | 🟡 Medium | ✅ |
| 10 | [Brute-forcing a stay-logged-in cookie](./authentication/10-brute-forcing-stay-logged-in-cookie/) | 🟡 Medium | ✅ |
| 11 | [Offline password cracking](./authentication/11-offline-password-cracking/) | 🟡 Medium | ✅ |
| 12 | [Password reset poisoning via middleware](./authentication/12-password-reset-poisoning-middleware/) | 🔴 Hard | ✅ |
| 13 | [Broken brute-force protection, multiple credentials per request](./authentication/13-multiple-credentials-per-request/) | 🔴 Hard | ✅ |
| 14 | [2FA bypass using a brute-force attack](./authentication/14-2fa-bypass-brute-force/) | 🔴 Hard | ✅ |

---

### 📁 File Upload Vulnerabilities — [6 labs](./file-upload-vulnerabilities/)

> Upload malicious files by bypassing server-side validation to achieve Remote Code Execution (RCE).

| # | Lab | Difficulty | Status |
|---|-----|:----------:|:------:|
| 1 | [Remote Code Execution via Avatar Upload](./file-upload-vulnerabilities/01-rce-via-avatar-upload/) | 🟢 Easy | ✅ |
| 2 | [Web Shell Upload via Content-Type Restriction Bypass](./file-upload-vulnerabilities/02-content-type-restriction-bypass/) | 🟢 Easy | ✅ |
| 3 | [Web Shell Upload via Path Traversal](./file-upload-vulnerabilities/03-path-traversal-bypass/) | 🟡 Medium | ✅ |
| 4 | [Web Shell Upload via Extension Blacklist Bypass](./file-upload-vulnerabilities/04-extension-blacklist-bypass/) | 🟡 Medium | ✅ |
| 5 | [Web Shell Upload via Obfuscated File Extension](./file-upload-vulnerabilities/05-obfuscated-file-extension/) | 🟡 Medium | ✅ |
| 6 | [Remote Code Execution via Polyglot Web Shell Upload](./file-upload-vulnerabilities/06-polyglot-web-shell/) | 🔴 Hard | ✅ |

---

### 🔵 Server-Side Request Forgery (SSRF) — [5 labs](./ssrf/)

> Trick the server into making HTTP requests to internal services, admin panels, or cloud metadata endpoints.

| # | Lab | Difficulty | Status |
|---|-----|:----------:|:------:|
| 1 | [Basic SSRF against the local server](./ssrf/01-basic-ssrf-local-server/) | 🟢 Easy | ✅ |
| 2 | [Basic SSRF against another back-end system](./ssrf/02-basic-ssrf-backend-system/) | 🟢 Easy | ✅ |
| 3 | [SSRF with blacklist-based input filter](./ssrf/03-ssrf-blacklist-bypass/) | 🟡 Medium | ✅ |
| 4 | [SSRF with filter bypass via open redirection](./ssrf/04-ssrf-open-redirection-bypass/) | 🟡 Medium | ✅ |
| 5 | [Blind SSRF with out-of-band detection](./ssrf/05-blind-ssrf-out-of-band/) | 🟡 Medium | ✅ |

---

### 🔴 Web Cache Deception — [4 labs](./web-cache-deception/)

> Craft URLs that trick caching servers into storing sensitive user responses, leaking API keys and session tokens.

| # | Lab | Difficulty | Status |
|---|-----|:----------:|:------:|
| 1 | [Exploiting path mapping for web cache deception](./web-cache-deception/01-exploiting-path-mapping/) | 🟡 Medium | ✅ |
| 2 | [Exploiting path delimiters for web cache deception](./web-cache-deception/02-exploiting-path-delimiters/) | 🟡 Medium | ✅ |
| 3 | [Exploiting origin server normalization for web cache deception](./web-cache-deception/03-origin-server-normalization/) | 🔴 Hard | ✅ |
| 4 | [Exploiting cache server normalization for web cache deception](./web-cache-deception/04-cache-server-normalization/) | 🔴 Hard | ✅ |

---

### 🟠 WebSockets — [3 labs](./websockets/)

> Exploit insecure real-time bidirectional connections via XSS injection, handshake manipulation, and cross-site hijacking.

| # | Lab | Difficulty | Status |
|---|-----|:----------:|:------:|
| 1 | [Manipulating WebSocket messages to exploit vulnerabilities](./websockets/01-manipulating-websocket-messages/) | 🟢 Easy | ✅ |
| 2 | [Manipulating the WebSocket handshake to exploit vulnerabilities](./websockets/02-manipulating-websocket-handshake/) | 🟡 Medium | ✅ |
| 3 | [Cross-site WebSocket hijacking](./websockets/03-cross-site-websocket-hijacking/) | 🔴 Hard | ✅ |

---

## 🎓 Learning Path

Follow this progression for a structured introduction to web security:

```
1️⃣  Authentication          → Understand how login flows can be broken
        ↓
2️⃣  File Upload Vulns       → Learn how file validation can be bypassed for RCE
        ↓
3️⃣  SSRF                   → Pivot from the browser to internal infrastructure
        ↓
4️⃣  Web Cache Deception     → Exploit caching layers to leak sensitive data
        ↓
5️⃣  WebSockets             → Attack real-time connections and cross-origin trust
```

> **Tip:** Each category builds on the previous one. Start from the 🟢 Easy labs and work your way up to 🔴 Hard.

---

## 📖 How to Use

Each lab folder contains a `README.md` with:

- **🎯 Objective** — What the lab is testing
- **🧠 Vulnerability Explained** — Background on the attack technique
- **🪜 Step-by-step Walkthrough** — Full exploitation guide with Burp Suite screenshots
- **💡 Key Takeaway** — The core lesson to remember

To use these writeups:

1. **Try the lab yourself first** on [PortSwigger Web Security Academy](https://portswigger.net/web-security)
2. **Refer to the writeup** if you get stuck — read the objective and walkthrough
3. **Compare your approach** with the solution to deepen your understanding

---

## 🛠️ Tools & Prerequisites

### Required Tools

| Tool | Purpose |
|------|---------|
| [Burp Suite Community/Pro](https://portswigger.net/burp) | HTTP proxy, Repeater, Intruder |
| A modern web browser | Lab interaction |

### Helpful Extras

| Tool | Purpose |
|------|---------|
| [exiftool](https://exiftool.org/) | Polyglot file creation (File Upload labs) |
| [Collaborator / interactsh](https://app.interactsh.com/) | Out-of-band callback detection (Blind SSRF) |

### Prerequisites

- Basic understanding of HTTP (requests, responses, headers, cookies)
- Familiarity with browser DevTools
- A free [PortSwigger Academy account](https://portswigger.net/users/register)

---

## 📬 Contact

<div align="center">

Made with ❤️ by [Mrdj30](https://github.com/Mrdj30)

[![GitHub](https://img.shields.io/badge/GitHub-Mrdj30-181717?style=for-the-badge&logo=github)](https://github.com/Mrdj30)

*⭐ Star this repo if you find it useful — it helps others discover these writeups!*

</div>
