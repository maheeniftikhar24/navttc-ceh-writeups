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
* Kali Linux (host operating system)

## Methodology

### 1. Connectivity Verification

Before testing the application, I verified that the target was reachable using:

```bash
ping testfire.net
```
<img width="1379" height="392" alt="image" src="https://github.com/user-attachments/assets/ec18a860-6d17-40ed-b414-9ecfe54c9f68" />
*Figure 1: Connectivity Verification using ping.*

### 2. Service Enumeration

I performed a basic Nmap scan to identify the services running on the target.

```bash
sudo nmap -p 80,443 -sV testfire.net
```
<img width="1600" height="469" alt="image" src="https://github.com/user-attachments/assets/c91919f2-9068-4727-9fad-50c5508e9e38" />
*Figure 2: Service enumeration using Nmap.*

### 3. Reconnaissance

I performed manual reconnaissance of the target application and identified the login page (`/login.jsp`) as a potential authentication endpoint for SQL Injection testing.
<img width="1774" height="990" alt="image" src="https://github.com/user-attachments/assets/5f765249-dcf0-4d84-b3f8-24bc32cc0b5e" />
*Figure 3: Target login page before testing.*

### 4. SQL Injection Testing

I tested the login form using common SQL Injection payloads to determine whether user input was properly validated and 

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

## Proof of Concept

The following screenshots demonstrate the successful authentication bypass.

### Step 1 – Target Login Page

<img width="1774" height="990" alt="image" src="https://github.com/user-attachments/assets/e02aade6-52d6-4967-85d9-fd7caf93f4a3" />

### Step 2 – SQL Injection Payload

```sql
' OR '1'='1' --

<img width="1772" height="976" alt="image" src="https://github.com/user-attachments/assets/73363d3a-bce1-4578-82c0-5f34693616af" />
















