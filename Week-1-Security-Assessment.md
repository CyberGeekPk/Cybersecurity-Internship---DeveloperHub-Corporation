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

---

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

### 4. Content Security Policy (CSP) Header Not Set
- **Observation**: Website isn't telling browsers what content (like scripts or images) it's allowed to load.
- **Risk**: High risk of getting hacked with bad code (XSS), which can steal user data or mess up the site.
- **Recommendation**: Set up a "Content Security Policy" to tell browsers exactly what content is safe to load.

---

### 5. Content Security Policy (CSP) Header Not Set
- **Observation**: The website is not using a Content Security Policy (CSP) header. This header tells web browsers what content (like scripts, images, and stylesheets) is allowed to load on the page. Without it, the browser doesn't know which sources are safe.
- **Risk**: **High**. This significantly increases the risk of Cross-Site Scripting (XSS) attacks. Attackers could inject malicious code, leading to data theft or website defacement.
- **Recommendation**: Implement a strict Content Security Policy (CSP) header. Define a whitelist of trusted sources for all content types (scripts, images, etc.) to prevent malicious injections.

---

### 6. Cross-Domain Misconfiguration
- **Observation**: The application's settings allow resources to be accessed from other websites without strong restrictions. This usually means the Cross-Origin Resource Sharing (CORS) policy is too broad.
- **Risk**: **High**. Overly permissive cross-domain settings can lead to data leaks or Cross-Site Request Forgery (CSRF) attacks, where malicious sites can make requests to application on behalf of a user.
- **Recommendation**: Review and restrict cross-domain access. Only allow specific, trusted domains to access resources. Avoid using wildcards (`*`) in CORS settings.

---

### 7. Hidden File Found
- **Observation**: Hidden files or directories (e.g., development files, backup files) were detected that are not meant for public access.
- **Risk**: **Medium**. These files can contain sensitive information like source code, configuration details, or credentials, which attackers could use to gain further access.
- **Recommendation**: Identify and remove or securely protect all hidden files and directories that are not intended for public viewing. Ensure web server is configured to prevent directory listings.

---

### 8. Cross-Domain JavaScript Source File Inclusion
- **Observation**: The application includes JavaScript code directly from external websites.
- **Risk**: **High**. If the external website providing the JavaScript code is compromised, malicious code could be injected application, leading to XSS or data theft.
- **Recommendation**: Carefully review all third-party JavaScript inclusions. Use Subresource Integrity (SRI) to verify that the external script hasn't been tampered with. Only use scripts from highly trusted and reputable sources.

---

### 9. Server Leaks Version Information via "Server" HTTP Response Header Field
- **Observation**: The web server is revealing its type and version number in the HTTP response headers (e.g., "Apache/X.Y.Z").
- **Risk**: **Low**. While not a direct vulnerability, this information helps attackers identify known weaknesses in specific server versions, making it easier for them to plan attacks.
- **Recommendation**: Configure the web server to hide or generalize the "Server" HTTP response header. This makes it harder for attackers to gather reconnaissance on your system.

---

### 10. Strict-Transport-Security Header Not Set
- **Observation**: The website is not using the HTTP Strict-Transport-Security (HSTS) header. This header forces web browsers to communicate with the site only over a secure HTTPS connection.
- **Risk**: **Medium**. Without HSTS, users are vulnerable to downgrade attacks and cookie hijacking if they initially try to connect over an insecure HTTP connection.
- **Recommendation**: Implement the `Strict-Transport-Security` header with an appropriate `max-age` value. Ensure entire application is fully accessible via HTTPS before enabling HSTS.

---

### 11. Timestamp Disclosure - Unix
- **Observation**: The application is exposing precise Unix timestamps, possibly in error messages or debugging information.
- **Risk**: **Low**. This information, while not directly exploitable, can provide subtle clues about system uptime or activity patterns to potential attackers.
- **Recommendation**: Review application outputs to remove unnecessary or precise timestamp disclosures. Use relative times or more general formats if timestamps are necessary.

---

### 12. Information Disclosure - Suspicious Comments
- **Observation**: Comments found in the application's code or public files may contain sensitive internal details, debugging information, or temporary notes.
- **Risk**: **Medium**. These comments can reveal internal logic, potential flaws, or even credentials, which can aid attackers in their reconnaissance efforts.
- **Recommendation**: Thoroughly review and remove all unnecessary or sensitive comments from production code and publicly accessible files. Implement code review processes to prevent such disclosures.

---

### 13. Modern Web Application
- **Observation**: This is an informational alert indicating that the target appears to be a modern web application, likely using contemporary frameworks or technologies.
- **Risk**: **Informational**. This is not a security risk but a classification of the application's nature.
- **Recommendation**: No specific security recommendation directly from this alert. Continue to apply robust security practices for modern web applications, focusing on API security, framework-specific vulnerabilities, and client-side security.

---

### 14. Re-examine Cache-control Directives
- **Observation**: The way the application handles caching (`Cache-Control` headers) might be incorrectly configured, potentially leading to sensitive data being cached or inefficient performance.
- **Risk**: **Low to Medium**. Improper caching can lead to sensitive user data being stored in public caches, making it accessible to others. It can also negatively impact website performance.
- **Recommendation**: Review and optimize `Cache-Control` headers. Ensure sensitive information is explicitly marked as non-cacheable (`no-store`, `no-cache`) and that static assets are cached effectively for performance.

---

### 15. User Agent Fuzzer
- **Observation**: ZAP performed a test by sending various malformed or unusual "User-Agent" header values to see how the application responds. This is a testing method, not a vulnerability.
- **Risk**: **Informational**. This alert simply confirms that the User-Agent fuzzing test was executed. Any specific vulnerabilities found during this test would be reported as separate alerts.
- **Recommendation**: Ensure the application handles all types of input, including unusual or malformed header values, gracefully and securely to prevent errors or unexpected behavior.

---

## Areas for Improvement

### 1. Strengthen Web Security Policies
- **Focus**: Implement crucial security headers and policies (like CSP, HSTS, and stricter CORS) to prevent common web attacks and enforce secure communication.

### 2. Control Information & File Exposure
- **Focus**: Prevent sensitive internal information (hidden files, revealing comments, precise timestamps) from being publicly accessible.

### 3. Secure External Resources & Caching
- **Focus**: Carefully manage third-party JavaScript includes and optimize caching settings to protect sensitive data and improve performance.

### 4. Improve Input Handling
- **Focus**: Ensure the application robustly handles all types of user input and avoids leaking information through errors.

---

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
6. I also used ZAP to perform automated vulnerability testing on target site and here are the results of that scan:
![image](https://github.com/user-attachments/assets/14604b31-2774-44c3-a35e-720e5077df8b)
 
