# ACME Agents

Agent ecosystem for security-testing the [ACME Demo](https://github.com/peteatpraxis/acme-demo) e-commerce application.

## Overview

This repository contains a collection of agents, subagents, skills, plugins, and hooks designed to audit, test, and report on security vulnerabilities in the ACME Demo application.

## Agents

| Agent | Description |
|---|---|
| [Security Auditor](.opencode/agents/security-auditor.md) | Full vulnerability scanning across the codebase |
| [Code Reviewer](.opencode/agents/code-reviewer.md) | PR review with security-focused analysis |
| [Penetration Tester](.opencode/agents/pentester.md) | Simulated attack scenario execution |
| [Dependency Scanner](.opencode/agents/dependency-scanner.json) | Dependency CVE detection |
| [Compliance Checker](.opencode/agents/compliance-checker.json) | OWASP Top 10 and CWE compliance validation |

## Subagents

| Subagent | Parent | Focus |
|---|---|---|
| [SQL Injection Tester](.opencode/subagents/sql-injection-tester.md) | Security Auditor | SQL query analysis and injection testing |
| [XSS Scanner](.opencode/subagents/xss-scanner.json) | Security Auditor | Cross-site scripting detection |
| [Auth Flow Tester](.opencode/subagents/auth-flow-tester.md) | Penetration Tester | Authentication bypass and JWT testing |

## Skills

| Skill | Description |
|---|---|
| [Vuln Pattern Matching](.opencode/skills/vuln-pattern-matching.json) | Regex-based vulnerability pattern detection |
| [Report Generation](.opencode/skills/report-generation.md) | Security findings report templates |
| [API Testing](.opencode/skills/api-testing.json) | REST endpoint testing methodology |

## Plugins

| Plugin | Description |
|---|---|
| [DB Inspector](.opencode/plugins/db-inspector.toml) | SQLite schema and data inspection |
| [Log Analyzer](.opencode/plugins/log-analyzer.json) | Security event log parsing |

## Hooks

| Hook | Trigger | Action |
|---|---|---|
| [Pre-commit Security](.opencode/hooks/pre-commit-security.json) | Pre-commit | Block commits with hardcoded secrets |
| [Post-scan Notify](.opencode/hooks/post-scan-notify.md) | Post-scan | Generate findings summary |

## Quick Start

1. Clone the [ACME Demo](https://github.com/peteatpraxis/acme-demo) repository
2. Install the agent configs into your project
3. Run the Security Auditor agent to begin scanning

## License

MIT
