# Week 3 Report: Advanced Security

## Overview

The focus for Week 3 was on strengthening the security posture of the application through practical penetration testing, implementing robust logging mechanisms, and establishing a security checklist based on best practices. The tasks executed were:

- Performing basic penetration testing using tools like **Nmap** and browser-based tools.
- Setting up application-level logging with the **Winston** logging library in Node.js.
- Creating and applying a security checklist for auditing.

---

## 1. Basic Penetration Testing

### Objectives

- Identify common vulnerabilities in the web application.
- Simulate attack vectors that could be exploited by malicious actors.
- Establish a baseline for application resilience against unauthorized access or data breaches.

### Tools and Techniques Used

#### Nmap (Network Mapper)

- **Purpose**: To identify open ports, running services, and potential vulnerabilities in the network layer.
- **Command Used**: nmap -sS -sV -T4 <target-ip>
- **Results:** Discovered open ports: 80 (HTTP), 443 (HTTPS)
- Confirmed only essential services are exposed.

#### Browser-based Testing
- **Tools Used:** Chrome Developer Tools, OWASP ZAP
- **Tests Performed:** Input field manipulation to detect potential XSS (Cross-Site Scripting), form tampering and session management validation.
- **Outcome:** Input sanitization implemented effectively in most fields.
- Sessions are secured and HTTP-only cookies are enabled.

---

## 2. Setting Up Basic Logging
Logging is a crucial part of application security. It provides visibility into the application’s behavior, helps in identifying anomalies, and supports incident response activities.

### Technology Used: Winston Logging Library
- Installation: npm install winston
- **Features Enabled**
- Timestamped logs for traceability
- Console and file-based log transport
- Centralized security-related logging in security.log
- Sample Log Output: 2025-06-01T10:32:00.501Z [INFO]: Application started

---

## 3. Security Checklist and Best Practices
A simple but effective checklist was created and reviewed to ensure critical security practices are being adhered to during development and deployment phases.

| Item                | Description                                                                                       | Status        |
|---------------------|---------------------------------------------------------------------------------------------------|---------------|
| Input Validation    | All user inputs are validated both client-side and server-side to prevent injection attacks.      | Implemented |
| HTTPS Enforcement   | All traffic is encrypted via HTTPS to secure data in transit.                                     | Configured  |
| Password Hashing    | Passwords are hashed using bcrypt and salted before storage in the database.                      | Completed   |
| Session Management  | Sessions are stored securely with HTTP-only cookies.                                              | In Place    |
| Logging             | Security events are logged using Winston for later auditing.                                      | Enabled     |
| Error Handling      | Sensitive error messages are hidden from the user to avoid information leakage.                   | Handled     |
| Dependency Scanning | Third-party packages are scanned for known vulnerabilities using npm audit.                      | Performed   |

---

## Summary
The security of the application has been significantly improved in Week 3 through targeted penetration testing, enhanced logging, and strict adherence to security best practices. These efforts lay a strong foundation for maintaining application integrity, confidentiality, and availability in future stages of development and deployment.
