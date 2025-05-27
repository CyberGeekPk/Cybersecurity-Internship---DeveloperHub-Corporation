# Security Measures Implementation Report: Vulnerable User Management Application
**Date:** May 27, 2025
**Application:** Simple User Management Web App (Self-Hosted)
**Phase:** Week 2 - Implementing Security Measures 

## 1. Introduction
This document outlines the vulnerabilities in a locally hosted simple user management web application and the security measures taken to 
 patch these vulnerabilities related to input handling, password storage, and access control.

## 2. Vulnerabilities Found
During the assessment, the following key vulnerabilities were identified:

### 2.1. Cross-Site Scripting (XSS) via Unsanitized Input
**Description:** 
The application's signup form (and potentially other input fields) does not properly sanitize user-supplied data before it is processed or stored. This allows malicious scripts to be injected into the application.

**Observation:** 
When attempting to register a user with a username containing a JavaScript payload (e.g., <script>alert('XSS Vulnerable!');</script>), the server accepts and stores this raw input. If this username were later displayed on a page without proper encoding or sanitization, the injected script would execute in the user's browser. While our current profile.html doesn't display the username, the vulnerability exists at the input processing level.

**Impact:** 
Could lead to session hijacking, defacement of the website, redirection to malicious sites, or execution of arbitrary code in the user's browser.

### 2.2. Weak Password Storage (Plain Text)
**Description:** 
User passwords are being stored in the application's mock database (a simple array in app.js) in plain, unhashed text.

**Observation:** 
After a user registers, the server-side console.log statement clearly outputs the users array, revealing the exact password provided by the user.

**Impact:** 
In the event of a database breach or unauthorized access to the server-side code, all user passwords would be immediately compromised, posing a severe security risk. This makes users susceptible to credential stuffing attacks if they reuse passwords across different services.

### 2.3. Simple Security Misconfiguration (Insecure Direct Object Reference / Broken Access Control)
**Description:** 
The /profile route, intended for authenticated users, can be accessed directly by any user simply by typing the URL into the browser, without requiring prior login or a valid session/token.

**Observation:** 
Even after restarting the server or opening a new incognito window (where no login has occurred), navigating to http://localhost:3000/profile successfully loads the profile page.

**Impact:** 
Sensitive information or functionalities intended only for authenticated users could be exposed to unauthorized individuals, leading to data breaches or unauthorized actions.

### 2.4. Lack of Secure HTTP Headers
**Description:** 
The application does not implement robust HTTP security headers, leaving it vulnerable to various client-side attacks.

**Observation:** 
Inspecting the network requests in browser developer tools (e.g., for index.html or app.js) reveals a lack of headers such as X-Content-Type-Options, X-Frame-Options, Strict-Transport-Security, and X-XSS-Protection.

**Impact:** 
This absence can make the application more susceptible to attacks like Clickjacking, MIME-type sniffing, cross-site scripting, and downgrade attacks.

## 3. Areas for Improvement (Proposed Fixes for Week 2)
Based on the identified vulnerabilities, the following security measures are recommended for implementation:

### Input Sanitization and Validation: 
Implement server-side input validation and sanitization for all user-supplied data (e.g., usernames, passwords) to prevent XSS and other injection attacks. Libraries like validator.js can be used.

### Password Hashing: 
Store user passwords using a strong, one-way hashing algorithm with a salt (e.g., bcrypt) instead of plain text.

### Enhanced Authentication and Access Control: 
Implement a robust authentication mechanism, such as token-based authentication (e.g., JSON Web Tokens - JWT), to secure routes and ensure that only authenticated and authorized users can access protected resources like the profile page.

### Secure HTTP Headers: 
Utilize a security middleware (e.g., helmet.js for Express) to automatically set appropriate HTTP response headers to enhance the application's security posture against common web vulnerabilities.
