# Extension: Security Audit

Purpose
- Enforce security best practices, crucial for projects handling sensitive data.
- To be used when project constraints include High Data Sensitivity or Compliance requirements.

Rules
- Never hardcode secrets, API keys, or passwords in the source code. Use environment variables.
- All data in transit must be encrypted using TLS/HTTPS.
- Validate and sanitize all user inputs to prevent SQL Injection, XSS, and other injection attacks.
- Implement robust authentication and authorization mechanisms.
- Regularly scan dependencies for known vulnerabilities (e.g., using `npm audit` or similar tools).
- Apply principle of least privilege for database access and internal service communication.
