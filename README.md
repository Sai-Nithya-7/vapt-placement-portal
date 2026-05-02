# VAPT Report: Placement Portal

Gray-box penetration test conducted against a self-developed Flask 
recruitment web application. Full source code was available to the tester.

## What was tested

A three-role placement portal (Admin, Company, Student) built with Flask, 
SQLAlchemy, and SQLite. All authenticated and unauthenticated routes were 
in scope: REST API endpoints, file upload, authentication, and RBAC.

## Methodology

OWASP Testing Guide v4. 

Phases: source code review → manual endpoint testing → authentication testing → access control testing → API security testing.

Tools: Nmap, Burp Suite Community, browser DevTools, PowerShell scripting, 
Flask server log analysis.

## Findings

| ID | Title | Severity |
|---|---|---|
| VULN-002 | Werkzeug interactive debugger exposed → arbitrary code execution | Critical |
| VULN-001 | Broken access control + runtime crash in `/api/applications` | High |
| VULN-005 | No rate limiting on login endpoint | Medium |
| VULN-006 | Hardcoded secret key fallback enables session forgery | Medium |
| VULN-003 | Missing explicit role check on resume serving endpoint | Low |
| VULN-004 | HR contact PII in unauthenticated public API response | Low |
| VULN-007 | User enumeration via registration form error messages | Informational |

Full findings with reproduction steps, CVSS scores, evidence, and 
remediation guidance are in [PENETRATION_TEST_REPORT_v1.pdf](./PENETRATION_TEST_REPORT_v1.pdf).

## What held up

CSRF protection blocked all automated POST attempts. File upload 
validation correctly rejected non-PDF files at the magic byte level, 
not just extension. Student-to-student IDOR on resume access was 
explicitly prevented.

## Repo structure
``` text
/vapt-placement-portal
  PENETRATION_TEST_REPORT_v1.pdf
  /evidence
    /screenshots
    flask_logs.txt
```

## Note

The target application is a separate repository:
[24f2000969/PlacementPortal](https://github.com/24f2000969/PlacementPortal)
