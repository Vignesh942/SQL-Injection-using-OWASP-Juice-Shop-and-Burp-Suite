
# SQL Injection Practice using OWASP Juice Shop and Burp Suite

## Overview
This repository documents hands on practice of SQL Injection (SQLi) using OWASP Juice Shop as the vulnerable application and Burp Suite for interception and testing.

The focus is on understanding how SQL injection works in real applications, not just theory.

---


## Lab Environment
- Target Application: OWASP Juice Shop (Local)
- URL: http://localhost:3000
- Tool: Burp Suite Community Edition
- Attack Type: SQL Injection (Authentication Bypass)

---

## Objective
- Identify user-controlled input points
- Intercept and analyze HTTP requests
- Manually test SQL injection payloads
- Observe application behavior and impact
- Understand root cause and prevention

---

## Attack Surface
Endpoint:
POST /rest/user/login

User-controlled parameters:
- email
- password

---

## Exploitation Steps

### Step 1: Intercept Login Request
- Burp Proxy enabled
- Login request captured
- Request sent to Repeater

### Step 2: Inject SQL Payload
Payload used in email field:
{
  "email": "' OR 1=1--",
  "password": "test"
}

### Step 3: Analyze Response
- Server returned HTTP 200 OK
- Authentication bypassed
- Valid JWT token received
- Logged in as admin user

---

## Why the Vulnerability Exists
- User input directly embedded into SQL queries
- No parameterized queries
- Improper input handling
- Application logic trusted client input

The database was not attacked directly.  
The application was manipulated into sending a modified query.

---

## Impact
- Unauthorized admin access
- Session token issued
- Potential exposure of sensitive data

---

## Prevention
- Use parameterized queries (prepared statements)
- Avoid SQL string concatenation
- Apply least-privilege database access
- Hide database error messages
- Perform regular security testing

---

## Learning Outcome
- Practical understanding of SQL injection
- Manual testing using Burp Suite
- Clear view of how simple coding mistakes lead to critical vulnerabilities




<img width="1919" height="1079" alt="Screenshot 2026-01-03 195544" src="https://github.com/user-attachments/assets/e1e10777-2783-4a4c-adbf-1b616c77dcf8" />


---
<img width="1915" height="1023" alt="Screenshot 2026-01-03 203430" src="https://github.com/user-attachments/assets/3cec79ec-ed40-43ce-bf46-da43e0565486" />




## Disclaimer
This activity was performed on an intentionally vulnerable application in a controlled lab environment for educational purposes only.
