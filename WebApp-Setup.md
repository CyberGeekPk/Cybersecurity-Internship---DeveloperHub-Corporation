# Web App Setup for Security Testing

# 1. Finding a Mock Web Application for Cybersecurity Testing
There are alot of delibrate vulnerable web apps on Internet for learning and security testing purposes. I selected *Juice Shop* for this task.

### Why Juice Shop?
#### 1. Specifically Designed for Security Testing
- Juice Shop is intentionally insecure, making it perfect for learning.
- It includes a wide range of realistic vulnerabilities (XSS, SQLi, authentication flaws, etc.).
- It aligns with the OWASP Top 10 — the industry standard for web security.


#### 2. Modern Tech Stack
- Built with Node.js, Express, and Angular, it resembles many modern web apps.
- This makes your testing experience more relevant to real-world scenarios.


#### 3. Easy to Set Up
- No need for complex configuration or database setup.
- Just:
- npm install
- npm start
- And you’re running.


#### 4. Guided Learning Tools
- Has built-in challenge tracking — the app shows which vulnerabilities you’ve found.
- Useful for both manual testing and automated scanning (e.g., with OWASP ZAP).


#### 5. Widely Accepted in Cybersecurity Learning
- Used in universities, CTF competitions, and official OWASP training events.
- Helps you build a credible portfolio — recruiters recognize Juice Shop.


#### 6. Open Source with Active Support
- Actively maintained by the OWASP community.
- Well-documented with a GitHub repo and official website: https://owasp.org/www-project-juice-shop/

# 2. Set Up the Application Locally
Here is how we can setup Juice Shop Web-app locally on our system.
### Step 1: Download and Install Node.js and Git
- First we have to install Node.js from https://nodejs.org/ to run Juice Shop
![image](https://github.com/user-attachments/assets/06825c70-5904-42ff-b8a7-a5950a22fcd6)

### Step 2: Cloning Juice Shop
- Now, we will clone Juice Shop and install it from this link: https://github.com/juice-shop/juice-shop.git
![image](https://github.com/user-attachments/assets/384f2702-6584-4d4f-b02b-43548518eea2)

- Juice shop is installed successfully, now we are goig to start it using: npm start

### Step 3: Run Juice Shop Web-app
- Open your browser and go to: http://localhost:3000
- You should see the Juice Shop interface.
