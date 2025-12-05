# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.2.x   | :white_check_mark: |
| 1.1.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

We take security seriously. If you discover a security vulnerability in the AI Bootstrap System, please report it responsibly.

### How to Report

**Please DO NOT open a public GitHub issue for security vulnerabilities.**

Instead:

1. **Email**: Send details to [security@yourdomain.com] (replace with your actual email)
2. **Include**:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if you have one)
3. **Timeline**: We'll acknowledge within 48 hours and provide updates

### What to Expect

- **Acknowledgment**: Within 48 hours
- **Initial Assessment**: Within 1 week
- **Fix Timeline**: Depends on severity
  - Critical: 1-7 days
  - High: 1-4 weeks
  - Medium: 4-12 weeks
  - Low: Best effort

### Security Considerations in This Framework

The AI Bootstrap System includes security-aware features:

#### Built-in Security Guardrails

1. **Secret Detection** (Section 6.5)
   - AI agents are instructed to never hardcode secrets
   - Preferring environment variables
   - Avoiding secrets in logs, errors, or comments

2. **High-Risk Classification** (Section 6.3)
   - Auth/authz changes require human approval
   - Security-sensitive code is flagged
   - Production configs are protected

3. **Audit Trails** (Sections 8, 10)
   - All changes logged in `SESSION_NOTES.md`
   - Risk classifications documented
   - Compliance mode available

#### Security Best Practices for Users

When using this framework:

✅ **DO:**
- Review all AI-generated code before deployment
- Use the HIGH RISK classification for security-sensitive areas
- Enable Compliance Mode for regulated environments
- Store secrets in environment variables or secret managers
- Regularly audit `SESSION_NOTES.md` for security changes

❌ **DON'T:**
- Trust AI agents with production credentials
- Allow unreviewed HIGH RISK changes to deploy
- Commit secrets to version control
- Disable security checks for convenience

#### Known Limitations

- AI agents may not catch all security vulnerabilities
- Human review is REQUIRED for security-critical code
- This framework is a process tool, not a security scanner
- Always use proper security tooling (SAST, DAST, etc.)

## Security Updates

Security patches will be:
- Released as soon as possible
- Announced in GitHub Security Advisories
- Documented in release notes
- Backported to supported versions when feasible

## Responsible Disclosure

We appreciate security researchers and will:
- Acknowledge your contribution (unless you prefer anonymity)
- Keep you updated on fix progress
- Credit you in release notes (with permission)

## Security Resources

- [AI_RULES_AND_BEST_PRACTICES.md](./AI_RULES_AND_BEST_PRACTICES.md) - Section 6.5: Security Considerations
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [CWE Top 25](https://cwe.mitre.org/top25/)

---

**Thank you for helping keep AI Bootstrap System and its users safe!**
