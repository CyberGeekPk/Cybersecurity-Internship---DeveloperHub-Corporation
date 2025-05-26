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

### 2. Cross-Site Scripting (XSS)
- **Location**: Search field
- **Payload Used**: `<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg/onload=alert('XSS')>
"><script>alert('XSS')</script>`
- **Impact**: Allows arbitrary JavaScript execution
- **Recommendation**: *Sanitize user input* using allowlists (not blocklists) and *apply Content Security Policy (CSP)*.

---

### 3. SQL Injection - Login Bypass
- **Location**: Login form
- **Payload**: `admin' OR '1'='1`
- **Impact**: Bypasses authentication, unauthorized access to user/admin accounts
- **Recommendation**: Use *parameterized queries* or *prepared statements*

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

1. Site is accepting week passwords in signup and login form.
2. I tried `<script>alert('XSS');</script>` but it showed normal results, This suggests basic input sanitization is in place, at least in the search field.
![image](https://github.com/user-attachments/assets/1d638001-bb4d-4918-8c0c-499065af9183)
3. Now, I will try a different payload version, lets see how it works
`<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg/onload=alert('XSS')>
"><script>alert('XSS')</script>` and the result is this, that's a successful XSS discovery! It means that Cross-Site Scripting (XSS) vulnerabilities exist in the Juice Shop application.
![image](https://github.com/user-attachments/assets/07bbceea-4504-431d-bf83-fd86d5794bd3)
4. Now I'll try to bypass login by using basic SQL injection `admin' OR '1'='1`
![image](https://github.com/user-attachments/assets/7a7b8b0e-ff05-4969-a17d-4b4b823f1da1)
5. This login is successful so this website is also vulnerable to SQL Injection attacks:
![image](https://github.com/user-attachments/assets/efcaaf2c-199a-4078-8efe-37ca6be2c29a)

