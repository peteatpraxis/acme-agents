# Auth Flow Tester Subagent

## Parent Agent

Penetration Tester

## Role

Specialized subagent for testing authentication and authorization mechanisms in the ACME Demo application.

## Test Scenarios

### Scenario 1: JWT None Algorithm Bypass

**Target**: `server/middleware/auth.js`

The middleware accepts `alg: none` in JWT verification:
```javascript
jwt.verify(token, JWT_SECRET, { algorithms: ['HS256', 'none'] }, ...)
```

**Test**:
1. Craft a JWT with header `{"alg":"none","typ":"JWT"}` and empty signature
2. Send request with `Authorization: Bearer <forged_token>`
3. Verify if the token is accepted

**Expected Result**: Token accepted without valid signature

### Scenario 2: Hardcoded Secret Exploitation

**Target**: `server/routes/auth.js`, `server/middleware/auth.js`

JWT secret is hardcoded as `supersecret123`.

**Test**:
1. Sign arbitrary claims with the known secret
2. Forge admin-level tokens: `{"userId":1,"role":"admin"}`
3. Access admin-only endpoints

**Expected Result**: Full privilege escalation

### Scenario 3: IDOR on Orders and Users

**Target**: `server/routes/checkout.js`, `server/routes/auth.js`

**Test**:
1. Authenticate as user `john` (id: 2)
2. Request `GET /api/checkout/1` (order belonging to admin)
3. Request `GET /api/auth/users` (all user data)

**Expected Result**: Access to other users' data without authorization

### Scenario 4: Password Exposure

**Target**: `server/routes/auth.js` login response

**Test**:
1. Login with valid credentials
2. Inspect response body for `password` and `api_key` fields

**Expected Result**: Plaintext password and API key returned in response

### Scenario 5: No Token Expiration

**Target**: `server/routes/auth.js`

**Test**:
1. Obtain a JWT token
2. Wait indefinitely (tokens never expire)
3. Use token for authenticated requests

**Expected Result**: Token remains valid forever

## Remediation Checklist

- [ ] Remove `none` from JWT algorithms list
- [ ] Move JWT secret to environment variable with sufficient entropy
- [ ] Add `expiresIn` to JWT sign options
- [ ] Remove password and api_key from login response
- [ ] Add authorization middleware to all protected routes
- [ ] Implement ownership checks on order and user endpoints
