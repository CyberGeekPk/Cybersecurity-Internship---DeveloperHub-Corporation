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
