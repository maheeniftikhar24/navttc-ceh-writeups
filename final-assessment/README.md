## Introduction

After completing the 3-month **NAVTTC Certified Ethical Hacker (CEH)** training, I appeared for the final national-level assessment on **13 May 2026**. Before the exam, I searched online for candidates' experiences and practical insights but found very little information. That's what inspired me to document my own experience.

In this write-up, I'll share my experience of the complete assessment, including the **20-mark MCQ exam** and the **80-mark practical lab exam**. I'll cover the assessment format, time management, the practical task I received, tasks assigned to other students, the demo and viva process, and some preparation tips that I hope will help future candidates.

## Assessment Overview

The final assessment was conducted on **13 May 2026** as part of the NAVTTC CEH program.

### Assessment Structure

| Component            | Marks |   Duration |
| -------------------- | ----: | ---------: |
| Theory (MCQs)        |    20 | 30 minutes |
| Practical (Lab Exam) |    80 |  3.5 hours |

### Schedule

* **Reporting Time:** 1:00 PM
* **Assessment Start:** 2:00 PM
* **Official End Time:** 6:00 PM

Although the assessment was scheduled to end at **6:00 PM**, students were called one by one to demonstrate their practical work and answer questions during a short viva. Because of this, many students, including myself, stayed until around **7:30–8:00 PM** before leaving.

## Theory Exam

The theory exam consisted of **20 MCQs** to be completed within **30 minutes**. Each student received a different question paper, so the questions varied from candidate to candidate.

The questions covered topics from throughout the 3-month NAVTTC CEH training. Some of the topics I remember include:

- SQL Injection
- DNS Enumeration
- Wi-Fi Security
- Aircrack-ng
- Nessus
- Web Application Firewall (WAF)
- Penetration Testing
- DDoS Mitigation
- Mobile Security
- Man-in-the-Middle (MITM)
- Ethical Hacking Methodology
- DoS
- Bug Bounty Programs

Overall, I found the theory section manageable. If you've understood the concepts covered during the training instead of memorizing them, you should be able to complete it comfortably within the given time.

## Practical Exam

The practical exam carried **80 marks** and lasted **3.5 hours**. Like the theory exam, each student received a **different practical task**, making every assessment unique.

After completing the practical task, candidates were called individually to **demonstrate their work** and answer questions during a **viva**. Since the demonstrations continued after the official exam time, female candidates were called first due to the late hours.

In addition to completing the task, we were required to prepare **two separate reports**:

1. **Detailed Technical Report (PDF):** Submitted to the examiner during the demo. It included the methodology, commands used, screenshots, findings, explanation of the vulnerability, remediation recommendations, and other technical details.

2. **One-Page Written Report:** A handwritten summary submitted to the **NAVTTC assessor**, briefly describing the assigned task, the approach followed, and the outcome.

The examiner reviewed the practical implementation, asked questions about the methodology, and assessed our understanding of the assigned task. Because of this process, many students, including myself, left around **7:30–8:00 PM**, even though the official assessment ended at **6:00 PM**.

### My Practical Task

The task assigned to me was:

> **Write a simple SQL Injection payload to bypass login and explain why it works.**

To remain within ethical and legal boundaries, I selected the intentionally vulnerable training application **http://testfire.net/** as my target.

My approach included:

* Verifying connectivity to the target using **ping**.
* Performing service enumeration using **Nmap**.
* Testing the login functionality.
* Identifying the SQL Injection vulnerability.
* Demonstrating authentication bypass using different SQL injection payloads.
* Explaining why the payload worked and identifying the root cause of the vulnerability.
* Documenting the findings in both the detailed technical report and the one-page summary report.


