# SQL Injection Tester Subagent

## Parent Agent

Security Auditor

## Role

Specialized subagent for detecting and analyzing SQL injection vulnerabilities in the ACME Demo application.

## Analysis Targets

### 1. `server/routes/auth.js`

**Vulnerable Pattern**:
```javascript
const query = `INSERT INTO users (username, password, email) VALUES ('${username}', '${password}', '${email}')`;
```

**Attack Vectors**:
- Register endpoint: `username = "'); DROP TABLE users; --"`
- Login endpoint: `username = "' OR '1'='1' --"`
- Login endpoint: `password = "' OR '1'='1' --"`

**Impact**: Complete database compromise, data exfiltration, authentication bypass

### 2. `server/routes/products.js`

**Vulnerable Pattern**:
```javascript
const query = `SELECT * FROM products WHERE name LIKE '%${q}%' OR description LIKE '%${q}%'`;
```

**Attack Vectors**:
- Search parameter: `q = "' UNION SELECT * FROM users --"`
- Search parameter: `q = "'; UPDATE users SET role='admin' WHERE username='john' --"`

**Impact**: Data extraction from any table, data modification, privilege escalation

## Detection Rules

1. Flag any SQL query using template literals with variable interpolation
2. Flag any SQL query using string concatenation with `+` operator
3. Flag any use of `db.exec()` with user-controlled input
4. Verify all `db.prepare()` calls use parameterized queries (`?` placeholders)

## Remediation Pattern

```javascript
// BAD
const query = `SELECT * FROM users WHERE username = '${username}'`;

// GOOD
const user = db.prepare('SELECT * FROM users WHERE username = ?').get(username);
```
