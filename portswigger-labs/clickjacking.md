# Clickjacking Labs

Clickjacking is a malicious technique that tricks users into clicking on something different from what the user perceives, potentially compromising the user's security. PortSwigger Web Security Academy offers a range of labs focused on understanding and exploiting clickjacking vulnerabilities.

## Lab Objectives
1. Understand how clickjacking works.
2. Learn to exploit clickjacking vulnerabilities on various platforms.
3. Develop mitigation strategies to prevent clickjacking in web applications.

### Practical Examples
- **Frame Injection**: Testing how web applications react when they are embedded in `<iframe>` tags by malicious sites.
- **Exploit Demonstrations**: Simulating user interaction through hidden elements to demonstrate unintended actions.

### Prevention Techniques
- Use the `X-Frame-Options` HTTP header to prevent your site from being framed.
- Implement Content Security Policy (CSP) to control resources the user agent is allowed to load.

**Note**: Always test clickjacking vulnerabilities in a controlled environment and adhere to legal guidelines.