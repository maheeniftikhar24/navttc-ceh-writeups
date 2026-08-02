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

The following screenshots demonstrate the successful exploitation of the SQL Injection vulnerability during the practical assessment.

### Step 1 – Target Login Page

I navigated to the Altoro Mutual login page and identified the username field as the primary input for authentication testing.

<img width="1774" height="990" alt="image" src="https://github.com/user-attachments/assets/ae901f81-2557-47af-af14-c8334f460d18" />
*Figure 4: Target login page before testing.*

### Step 2 – SQL Injection Payload

The following payload was entered into the **username** field:

```sql
' OR '1'='1' --
```

The password field was populated with any random value('test' in my case), and the login request was submitted.

<img width="1772" height="976" alt="image" src="https://github.com/user-attachments/assets/64b8371b-525a-4de5-b114-d8ca9ace6e94" />
*Figure 5: SQL Injection payload entered into the login form.*

### Step 3 – Authentication Bypass

After submitting the payload, the application authenticated the session without requiring valid credentials, confirming that the login form was vulnerable to SQL Injection.

<img width="1777" height="1003" alt="image" src="https://github.com/user-attachments/assets/a39c1106-d41a-425b-8ca8-932bddd6e355" />
*Figure 6: Successful authentication bypass.*


The successful login confirmed that the application was vulnerable to **SQL Injection Authentication Bypass**, allowing unauthorized access by manipulating the SQL query used for user authentication.

> **Note:** This proof of concept was performed only against the intentionally vulnerable training application **http://testfire.net/** in an authorized lab environment as part of the NAVTTC CEH practical assessment.

## Root Cause

The application did not properly validate or sanitize user input before constructing SQL queries. As a result, the injected payload modified the query logic and bypassed authentication.

## Impact

A successful SQL Injection authentication bypass can allow an attacker to:

* Gain unauthorized access.
* Bypass authentication controls.
* Potentially access sensitive information.

## Remediation

* Use parameterized queries (prepared statements).
* Validate and sanitize user input.
* Apply the principle of least privilege to database accounts.
* Perform regular security testing.

## Lessons Learned

This exercise reinforced the importance of following a structured penetration testing methodology and demonstrated how improper input validation can lead to authentication bypass. It also highlighted the value of clear technical reporting and effectively communicating findings during the assessment.



