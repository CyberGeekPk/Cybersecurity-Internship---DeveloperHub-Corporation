# Week 1: Vulnerability Assessment Report

## Application Tested
- **App Name**: Juice Shop
- **URL**: https://demo.owasp-juice.shop/#/

---

## Tools Used
- OWASP ZAP
- Browser Dev Tools
- Manual Injection Scripts

---

## Vulnerabilities Found

### 1. Weak Password Policy
- **Location**: Signup form input field
- **Password Used**: `12345678`
- **Result**: Account is created successfully without any warning or enforcement of password complexity.
- **Impact**: Encourages insecure password habits, makes user accounts susceptible to brute-force and guessing attacks.
- **Recommendation**: Implement strong password policies like use of minimum 8 characters, at least one uppercase letter, one number, and one symbol and consider using NIST password guidelines.

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

## Assessment Steps
