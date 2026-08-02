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
