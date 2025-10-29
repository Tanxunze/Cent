# Security Policy

## Reporting Security Vulnerabilities

If you discover a security vulnerability in Cent, please report it by:

1. **Do NOT** open a public issue
2. Send a detailed report to the repository maintainers via GitHub Security Advisories
3. Include steps to reproduce, impact assessment, and any suggested fixes

We take all security reports seriously and will respond promptly.

## Security Audit

This repository has been audited for security vulnerabilities. See [SECURITY_AUDIT_REPORT.md](../SECURITY_AUDIT_REPORT.md) for the complete audit report.

### Last Audit
- **Date:** October 29, 2025
- **Status:** ✅ PASSED
- **Findings:** No malicious code or dependencies detected
- **Vulnerabilities Fixed:** 3 (all in Vite dev dependency)

## Security Best Practices

This project follows these security practices:

- ✅ Regular dependency updates
- ✅ No hardcoded secrets or credentials
- ✅ Secure data storage (client-side only, user-owned GitHub repos)
- ✅ No dangerous code execution patterns (eval, innerHTML, etc.)
- ✅ Proper authentication via GitHub OAuth
- ✅ Code linting and type checking

## Dependencies

All dependencies are regularly checked against the GitHub Advisory Database. We maintain:

- **59 total dependencies** (runtime + development)
- All from trusted sources (npm registry)
- Regular updates to patched versions
- No known vulnerabilities

## Data Privacy

Cent stores all user data in:
- **User's own GitHub repositories** - You maintain full control
- **Browser localStorage** - For preferences and authentication tokens
- **Browser IndexedDB** - For local caching

**We do not:**
- Store user data on third-party servers (except GitHub)
- Track user behavior
- Share data with third parties
- Use analytics without explicit consent

## Supported Versions

We recommend always using the latest version of Cent for the best security and features.

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |
| < Latest| :x:                |

## Security Updates

Security updates are released as soon as vulnerabilities are discovered and patched. Check the [releases page](https://github.com/Tanxunze/Cent/releases) for update notifications.
