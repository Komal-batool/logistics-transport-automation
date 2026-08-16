# Security & Privacy

This repository is a sanitized technical case study of a real-world logistics automation implementation.

The actual production environment contains private business information and credentials that are intentionally excluded.

---

# Sensitive Information

The following information must never be committed to the repository:

- API keys
- OAuth client secrets
- OAuth access tokens
- Refresh tokens
- Passwords
- Private webhook URLs
- Customer names
- Customer email addresses
- Customer telephone numbers
- Customer addresses
- Private Google Drive links
- Private spreadsheet information
- WhatsApp credentials
- PDF generation credentials

---

# Credential Management

Credentials should be stored using the secure credential mechanisms provided by the automation platform or the relevant external service.

Workflow logic should reference credentials rather than embedding secrets directly.

---

# Sanitized Portfolio Version

Any workflow or configuration shown publicly should replace sensitive values with placeholders.

Example:

```text
Production:

Authorization: Bearer REAL_ACCESS_TOKEN
