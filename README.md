# Web Application Security — OWASP Juice Shop

A web application security assessment project based on OWASP Juice Shop, completed as part of COMP H2704 – Web Application Security at TU Dublin.

The project involved vulnerability discovery and exploitation, vulnerability analysis, Static Application Security Testing (SAST), and Dynamic Application Security Testing (DAST).

## Overview

OWASP Juice Shop is an intentionally vulnerable web application used for security training and testing.

The assessment involved investigating the application's attack surface, solving security challenges, analysing selected vulnerabilities, and validating findings using automated security testing tools.

## Vulnerability Testing

The group completed a range of Juice Shop challenges covering different vulnerability classes.

My individual challenges included:

| Challenge | Vulnerability |
|---|---|
| Login Jim | SQL Injection |
| View Basket | Broken Access Control |
| DOM XSS | Cross-Site Scripting |
| Forgotten Sales Backup | Sensitive Data Exposure |
| Forged Coupon | Business Logic Flaw |

## Vulnerability Analysis

Two vulnerabilities were analysed in depth as part of my individual contribution:

### SQL Injection — Login Bypass

The login functionality was tested for SQL injection by examining how user-supplied input was processed.

The vulnerability allowed authentication to be bypassed by manipulating the SQL query through crafted input.

The analysis covered:

- Vulnerability description and root cause
- Investigation and testing process
- Exploitation behaviour
- Potential impact
- Recommended mitigation

The vulnerability was associated with OWASP A03: Injection and CWE-89.

### Broken Access Control — View Basket

The basket functionality was tested by examining requests made to the basket endpoint and modifying the basket identifier.

The application returned another user's basket without properly verifying resource ownership.

The analysis covered:

- Vulnerability description and root cause
- Investigation and testing process
- Exploitation behaviour
- Potential impact
- Recommended mitigation

The vulnerability was associated with OWASP A01: Broken Access Control.

## SAST — Semgrep

Static Application Security Testing was performed using Semgrep OSS 1.160.0 against the OWASP Juice Shop source code.

### Configuration

- Tool: Semgrep OSS 1.160.0
- Ruleset: `p/security-audit`
- Languages: TypeScript, JavaScript, JSON and Dockerfile
- Scope: Juice Shop application source
- Excluded directories: `node_modules/`, `frontend/`, `dist/`

The scan analysed 463 files and produced five blocking findings across four files.

Three findings were selected for deeper analysis:

1. Hardcoded RSA private key
2. Possible open redirect
3. Cross-Site Scripting in the video handler

An important limitation identified during the assessment was that the SAST scan did not detect the SQL injection vulnerability in `login.ts`. This demonstrated the importance of combining static analysis with dynamic testing and manual investigation.

## DAST — OWASP ZAP

Dynamic Application Security Testing was performed using OWASP ZAP 2.17.0.

The assessment used ZAP's Manual Explore functionality to capture application traffic before performing a targeted Active Scan.

The tested application areas included:

- Authentication
- Product search
- Customer feedback
- Complaint functionality
- Administration functionality

The scan produced:

- 1 High risk alert
- 6 Medium risk alerts
- 6 Low risk alerts
- 9 Informational alerts

### Key Findings

The most significant finding was SQL Injection affecting the product search endpoint.

Other findings included:

- Content Security Policy header not set
- Cross-domain misconfiguration
- JWT stored in browser local storage
- Missing anti-clickjacking headers
- Session ID in URL rewrite
- Missing Subresource Integrity attributes

Selected findings were manually validated against the running application.

## Tools Used

- OWASP Juice Shop
- Burp Suite
- Semgrep
- OWASP ZAP
- Browser Developer Tools
- jwt.io

## Security Concepts

The project provided practical experience with:

- SQL Injection
- Cross-Site Scripting
- Broken Access Control
- Sensitive Data Exposure
- Business Logic vulnerabilities
- JWT security
- Authentication weaknesses
- SAST
- DAST
- Manual vulnerability validation
- OWASP Top 10
- CWE

## Evidence

Screenshots and supporting evidence from the project are stored in the `screenshots/` directory.

Sensitive information, credentials, authentication tokens and personal academic information have been excluded from the public repository.

## Learning Outcomes

This project provided practical experience in identifying, exploiting, analysing and validating web application security vulnerabilities.

It also demonstrated the differences between manual security testing, SAST and DAST, including the importance of manually validating automated findings and understanding the limitations of automated security tools.

## Project Status

Completed as part of the COMP H2704 Web Application Security CA3 project.
