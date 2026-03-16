# Skill: Security Audit

> **Purpose:** Check code for security vulnerabilities and unsafe patterns
> **Used by:** Reviewer
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- Code has been written or modified
- A security-sensitive feature is being implemented (auth, payments, data handling)
- A security review is requested
- The Reviewer agent runs its review workflow

## Input

- Code to audit
- Context about what the code does

## Procedure

### Step 1: OWASP Top 10 Check
Review for each category:
1. **Injection** — SQL injection, command injection, XSS
2. **Broken Authentication** — Weak auth, session management
3. **Sensitive Data Exposure** — Unencrypted data, logging secrets
4. **XML External Entities** — XXE attacks
5. **Broken Access Control** — Missing authorization checks
6. **Security Misconfiguration** — Default credentials, verbose errors
7. **Cross-Site Scripting (XSS)** — Input sanitization
8. **Insecure Deserialization** — Untrusted data deserialization
9. **Known Vulnerabilities** — Outdated dependencies
10. **Insufficient Logging** — Missing audit trails

### Step 2: Code-Level Checks
1. Are secrets hardcoded? (API keys, passwords, tokens)
2. Are user inputs validated and sanitized?
3. Are SQL queries parameterized?
4. Are file paths validated (no path traversal)?
5. Are permissions checked on every protected operation?
6. Is sensitive data encrypted at rest and in transit?

### Step 3: Dependency Check
1. Are dependencies up to date?
2. Are there known vulnerabilities in dependencies?
3. Are dependency versions pinned?

### Step 4: Report Findings
Categorize findings:
- **Critical:** Must fix before deploy — active exploit possible
- **High:** Must fix soon — exploitable under specific conditions
- **Medium:** Should fix — defense-in-depth issue
- **Low:** Consider fixing — best practice improvement
- **Info:** No immediate risk — awareness item

## Output

- Security findings categorized by severity
- Remediation suggestions for each finding

## Project-Specific Notes

[NOT YET CONFIGURED] — After bootstrap: stack-specific security concerns, auth framework, etc.

## Quality Criteria

- [ ] All OWASP categories checked
- [ ] Code-level checks completed
- [ ] Dependencies reviewed
- [ ] Findings are actionable with remediation steps

## Improvement Log

[No entries yet — this log grows with use]
