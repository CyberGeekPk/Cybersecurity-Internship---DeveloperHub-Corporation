# Cybersecurity Internship - DeveloperHub Corporation
This repository documents the work completed during my cybersecurity internship. The goal is to identify and mitigate security vulnerabilities in a sample web application.

## Project Overview
**Task**: Strengthen the security posture of a user management web application.  
**Duration**: 6 Weeks  
**Tools Used**: OWASP ZAP, Browser Dev Tools, Manual Testing

---

## Weekly Tasks

### Week 1: Security Assessment
- Set up a mock web application
- Performed vulnerability assessment
- Identified potential issues (XSS, SQLi, weak storage)
- Documented findings and recommendations

Explore the detailed report in [`Week 1: Security Assessment`](./Week-1-Security-Assessment.md)

### Week 2: Security Measures Implementation
This report summarizes the security enhancements applied to a simple user management web application, addressing identified vulnerabilities.
#### Vulnerabilities Fixed:
- XSS: Input sanitization and validation implemented using validator.js.
- Weak Password Storage: Passwords are now securely hashed with bcrypt.js.
- Broken Access Control: Routes are protected using jsonwebtoken (JWT) for token-based authentication.
- Insecure HTTP Headers: helmet.js was integrated to add essential security headers.

Explore the detailed report in [`Week 2: Security Measures Implementation`](./Week-1-Security-Assessment.md)

---

## Web Application Setup

The application used for testing is a mock user management system. See setup instructions in [`WebApp-Setup`](./WebApp-Setup.md).

---

## 📚 Resources and Tools

- [OWASP ZAP](https://www.zaproxy.org/)
- [Common Vulnerabilities and Exposures (CVE)](https://cve.mitre.org/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

---
