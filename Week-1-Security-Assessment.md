# Week 1: Vulnerability Assessment Report

## Application Tested
- **App Name**: [Mock Web App Name]
- **URL**: http://localhost:3000

---

## Tools Used
- OWASP ZAP
- Browser Dev Tools
- Manual Injection Scripts

---

## Vulnerabilities Found

### 1. Cross-Site Scripting (XSS)
- **Location**: Signup form input field
- **Payload Used**: `<script>alert('XSS');</script>`
- **Impact**: Allows arbitrary script execution
- **Recommendation**: Sanitize user inputs

---

### 2. SQL Injection
- **Location**: Login form
- **Payload**: `' OR '1'='1`
- **Impact**: Bypasses authentication
- **Recommendation**: Use parameterized queries

---

### 3. Weak Password Storage
- **Observation**: Passwords stored in plain text
- **Risk**: High
- **Recommendation**: Hash passwords using bcrypt or Argon2

---

## Areas for Improvement
- Implement Content Security Policy (CSP)
- Use HTTPS locally (self-signed cert for testing)
- Enable HTTPOnly and Secure flags on cookies

