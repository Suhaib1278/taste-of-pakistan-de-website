---
trigger: always_on
---

# Standard Security Audit Checklist (SSAC)

This checklist must be completed by the **@security-specialist** for all high-impact features before a merge to `develop`. 

> **Goal:** To ensure no logical flaws or architectural gaps exist that could be exploited by an adversary.

---

## 1. Authentication & Session Management
- [ ] **Brute Force Resistance:** Are the `/login` and `/auth` endpoints rate-limited?
- [ ] **Credential Integrity:** Are all passwords and recovery keys hashed using **SHA-256** or better? (Audit the `AuthManager`).
- [ ] **Session Security:** Are session cookies or tokens set to `HttpOnly`, `Secure`, and `SameSite=Strict`?
- [ ] **IDOR (Insecure Direct Object Reference):** Can User A access User B's data by manipulating a URL ID or JSON payload (e.g., `user_id=101` vs `user_id=102`)?

## 2. Input Validation (The "Hacker's Gate")
- [ ] **SQL Injection:** Are all SQLite queries strictly parameterized? (Verify: **Zero** use of f-strings in SQL queries).
- [ ] **XSS (Cross-Site Scripting):** Is frontend data rendered via `textContent` rather than `innerHTML`?
- [ ] **Command Injection:** Does any user-supplied string reach `os.system()`, `subprocess.run()`, or `eval()`? (Strictly forbidden).
- [ ] **Path Traversal:** Can a user input a string like `../../etc/passwd` to read or write files outside the intended directory?

## 3. Cryptography & Data Protection
- [ ] **Encryption at Rest:** Are sensitive API keys (VPS, Monero, etc.) encrypted using the **Fernet** (Cryptography library) symmetric key?
- [ ] **Leakage in Logs:** Are raw secrets, plain-text keys, or PII (Personally Identifiable Information) excluded from the RAM-only logs?
- [ ] **Hardcoded Secrets:** Are there any API keys, salt strings, or secrets hardcoded in the source code? (Use `.env` files only).

## 4. Environment & Supply Chain
- [ ] **Dependency Audit:** Run `pip-audit` or `safety check` on `requirements.txt` to identify known vulnerabilities (CVEs).
- [ ] **CORS Policy:** Is the backend restricted to specific origins? Is `Access-Control-Allow-Origin: *` disabled?
- [ ] **Service Worker (PWA) Integrity:** Does `sw.js` correctly validate incoming requests to prevent malicious script injection?

---

## 5. Adversarial Reporting Template
When a vulnerability is found, the **@security-specialist** must output:
1. **Severity:** (P0: Critical, P1: High, P2: Medium)
2. **Exploit PoC:** A terminal command or script demonstrating the hack.
3. **Remediation:** The exact code change required to close the hole.
