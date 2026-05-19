# Report Generation Skill

## Purpose

Generate standardized security findings reports for the ACME Demo application.

## Report Template

```markdown
# Security Audit Report — ACME Demo

**Date**: {{DATE}}
**Scanner**: {{AGENT_NAME}}
**Target**: https://github.com/peteatpraxis/acme-demo
**Commit**: {{COMMIT_HASH}}

## Executive Summary

{{EXECUTIVE_SUMMARY}}

| Metric | Count |
|---|---|
| Critical | {{CRITICAL_COUNT}} |
| High | {{HIGH_COUNT}} |
| Medium | {{MEDIUM_COUNT}} |
| Low | {{LOW_COUNT}} |
| Info | {{INFO_COUNT}} |

## Findings

### Critical

{{CRITICAL_FINDINGS}}

### High

{{HIGH_FINDINGS}}

### Medium

{{MEDIUM_FINDINGS}}

### Low

{{LOW_FINDINGS}}

## OWASP Top 10 Mapping

| OWASP Category | Findings | Status |
|---|---|---|
| A01:2021 Broken Access Control | {{COUNT}} | FAIL |
| A02:2021 Cryptographic Failures | {{COUNT}} | FAIL |
| A03:2021 Injection | {{COUNT}} | FAIL |
| A04:2021 Insecure Design | {{COUNT}} | FAIL |
| A05:2021 Security Misconfiguration | {{COUNT}} | FAIL |
| A06:2021 Vulnerable Components | {{COUNT}} | FAIL |
| A07:2021 Auth Failures | {{COUNT}} | FAIL |
| A08:2021 Data Integrity | {{COUNT}} | FAIL |
| A09:2021 Logging Failures | {{COUNT}} | FAIL |
| A10:2021 SSRF | {{COUNT}} | FAIL |

## Recommendations

1. Replace all string-concatenated SQL queries with parameterized statements
2. Implement bcrypt or argon2 for password hashing
3. Move all secrets to environment variables or a secrets manager
4. Remove `none` from JWT algorithm allowlist
5. Add token expiration to all JWT tokens
6. Implement input validation and output encoding
7. Restrict CORS to specific origins
8. Remove stack traces from production error responses
9. Update all dependencies to latest patched versions
10. Add rate limiting to authentication endpoints

## Appendix

### CWE Reference

| CWE ID | Description | Count |
|---|---|---|
| CWE-89 | SQL Injection | 2 |
| CWE-79 | Cross-site Scripting | 2 |
| CWE-798 | Use of Hard-coded Credentials | 3 |
| CWE-918 | Server-Side Request Forgery | 1 |
| CWE-22 | Path Traversal | 1 |
| CWE-1321 | Prototype Pollution | 1 |
| CWE-362 | Race Condition | 1 |
| CWE-287 | Improper Authentication | 1 |
| CWE-256 | Plaintext Password Storage | 1 |
| CWE-209 | Error Information Exposure | 1 |
```
