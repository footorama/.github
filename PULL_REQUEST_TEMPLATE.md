# Security Pull Request Checklist

*This checklist is a mandatory part of our security review process. Address each point before requesting a merge.*

---

### Phase 1: Static Code Review (Before Merge)

*Developer & Reviewer must check these items in the code.*

- [ ] **Data Validation:** Is all untrusted input (from users, APIs, files) strictly validated for type, length, and format before use?
- [ ] **Injection Prevention:** Is data kept separate from queries and commands (e.g., using parameterized queries)? No string building for execution.
- [ ] **Access Control:** Does this code verify the user is **authorized** to access/modify *this specific data*? (Checks ownership, not just authentication).
- [ ] **Output Encoding:** Is all data sent to a browser properly encoded to prevent Cross-Site Scripting (XSS)?
- [ ] **Secrets Management:** Are secrets, tokens, and credentials loaded from a secure vault or environment variables? (No hardcoded secrets).
- [ ] **Dependency Scan:** Have new or updated dependencies been scanned for known vulnerabilities? (e.g., `npm audit`).

---

### Phase 2: Dynamic & Runtime Review (In Staging)

*To be checked by QA or a security champion on the running application.*

- [ ] **Automated Scan:** Has a DAST scan (e.g., OWASP ZAP) been run against the staging environment, with no new critical/high findings?
- [ ] **Manual Checks:**
    - [ ] Logged in as `User A`, can you access/modify `User B`'s data by guessing URLs?
    - [ ] Have you tested inputs with basic XSS and SQL injection payloads (`<script>`, `'`)?
    - [ ] Do error pages or API responses leak sensitive information (e.g., stack traces, config details)?

---
### Final Approval
- [ ] **Merge approved by (reviewer's @handle):**