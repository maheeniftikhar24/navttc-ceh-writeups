# SQL Injection Authentication Bypass

## Table of Contents

- [Objective](#objective)
- [Target](#target)
- [Tools Used](#tools-used)
- [Methodology](#methodology)
- [SQL Injection Payloads Tested](#sql-injection-payloads-tested)
- [Proof of Concept](#proof-of-concept)
- [Root Cause](#root-cause)
- [Impact](#impact)
- [Remediation](#remediation)
- [Lessons Learned](#lessons-learned)

## Objective

The objective of this assessment was to demonstrate a simple SQL Injection authentication bypass and explain why the payload works. To remain within ethical and legal boundaries, I performed this exercise against the intentionally vulnerable training application **http://testfire.net/**.

## Target

* **Target Application:** Altoro Mutual
* **URL:** http://testfire.net/
* **Target Type:** Intentionally vulnerable web application
* **Objective:** Demonstrate SQL Injection authentication bypass in an ethical lab environment.

## Tools Used

* Ping
* Nmap
* Web Browser
* Kali Linux working as a host os (you can use in in a vm environment as well)

## Methodology

### 1. Connectivity Verification

Before testing the application, I verified that the target was reachable using:

```bash
ping testfire.net
```
<img width="1379" height="392" alt="image" src="https://github.com/user-attachments/assets/ec18a860-6d17-40ed-b414-9ecfe54c9f68" />

### 2. Service Enumeration

I performed a basic Nmap scan to identify the services running on the target.

```bash
sudo nmap -p 80,443 -sV testfire.net
```

This helped identify the web service that would later be tested for SQL Injection vulnerabilities.

### 3. Reconnaissance

I explored the application manually and identified the login page https://testfire.net/login.jsp as a potential input point for authentication testing.

### 4. SQL Injection Testing

I tested the login form using several common SQL Injection payloads to determine whether authentication could be bypassed.

### 5. Authentication Bypass

After identifying a successful payload, I demonstrated that the application accepted the injected SQL statement and allowed authentication without valid credentials.

### 6. Documentation

Finally, I documented the methodology, screenshots, findings, impact, and remediation recommendations in the technical report submitted during the practical assessment.

## SQL Injection Payloads Tested

During the assessment, I tested multiple SQL Injection payloads against the login page to determine whether the application was vulnerable to authentication bypass.

| Payload           | Result                             |
| ----------------- | ---------------------------------- |
| `' OR '1'='1' --` | ✅ Successful Authentication Bypass |

### Successful Payload

```sql
' OR '1'='1' --
```

### Why It Works

A vulnerable application constructs SQL queries by directly concatenating user input into the database query. For example:

```sql
SELECT * FROM users
WHERE username = '[username]'
AND password = '[password]';
```

When the payload is entered into the username field, the query becomes:

```sql
SELECT * FROM users
WHERE username = '' OR '1'='1' --'
AND password = '';
```

Here's what happens:

* `'1'='1'` is always **TRUE**.
* The `OR` operator makes the authentication condition evaluate to **TRUE**.
* `--` comments out the rest of the SQL query, including the password check.
* As a result, the application may authenticate the user without requiring valid credentials.

> **Note:** This demonstration was performed only against the intentionally vulnerable training application **http://testfire.net/** as part of the NAVTTC CEH practical assessment.














