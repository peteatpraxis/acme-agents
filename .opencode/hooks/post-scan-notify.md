# Post-Scan Notification Hook

## Trigger

Executes after each security scan completes.

## Purpose

Generate a summary of scan findings and notify the team of new or changed vulnerabilities.

## Notification Template

```
?? ACME Demo Security Scan Complete

Scan ID: {{SCAN_ID}}
Date: {{TIMESTAMP}}
Agent: {{AGENT_NAME}}
Duration: {{DURATION}}

---

## Summary

| Severity | New | Changed | Resolved | Total |
|---|---|---|---|---|
| Critical | {{CRITICAL_NEW}} | {{CRITICAL_CHANGED}} | {{CRITICAL_RESOLVED}} | {{CRITICAL_TOTAL}} |
| High | {{HIGH_NEW}} | {{HIGH_CHANGED}} | {{HIGH_RESOLVED}} | {{HIGH_TOTAL}} |
| Medium | {{MEDIUM_NEW}} | {{MEDIUM_CHANGED}} | {{MEDIUM_RESOLVED}} | {{MEDIUM_TOTAL}} |
| Low | {{LOW_NEW}} | {{LOW_CHANGED}} | {{LOW_RESOLVED}} | {{LOW_TOTAL}} |

---

## New Critical Findings

{{NEW_CRITICAL_LIST}}

## New High Findings

{{NEW_HIGH_LIST}}

---

## Trend

{{TREND_ANALYSIS}}

---

## Actions Required

{{REQUIRED_ACTIONS}}

---
Full report: {{REPORT_URL}}
```

## Delivery Channels

| Channel | Config | Enabled |
|---|---|---|
| Console | stdout | true |
| File | `reports/scan-summary.md` | true |
| Slack | `#security-alerts` webhook | false |
| Email | `security-team@acme.com` | false |

## Threshold Rules

- If any **Critical** findings exist ? notify immediately
- If **High** findings increase by 2+ ? notify immediately
- If total findings decrease ? weekly digest only
- If no new findings ? no notification

## Example Output

```
?? ACME Demo Security Scan Complete

Scan ID: scan-20260519-001
Date: 2026-05-19T12:00:00Z
Agent: security-auditor
Duration: 45s

---

## Summary

| Severity | New | Changed | Resolved | Total |
|---|---|---|---|---|
| Critical | 0 | 0 | 0 | 5 |
| High | 0 | 0 | 0 | 6 |
| Medium | 0 | 0 | 0 | 4 |
| Low | 0 | 0 | 0 | 2 |

---

## Trend

No changes since last scan. 17 total findings remain unremediated.

## Actions Required

No new actions. All 17 findings are tracked in the backlog.

---
Full report: ./reports/full-scan-20260519-001.md
```
