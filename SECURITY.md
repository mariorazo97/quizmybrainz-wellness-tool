# Security Policy

## Supported Versions

We release patches for security vulnerabilities. Currently supported versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |

## Reporting a Vulnerability

We take the security of Body & Mind Detective seriously. If you discover a security vulnerability, please follow these steps:

### How to Report

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, please report them via email to:
- **Email**: [Your contact email - consider creating a security@quizmybrainz.com]

You should receive a response within 48 hours. If for some reason you do not, please follow up via email to ensure we received your original message.

### What to Include

Please include the following information in your report:

- Type of vulnerability (e.g., XSS, CSRF, injection)
- Full paths of source file(s) related to the vulnerability
- Location of the affected source code (tag/branch/commit or direct URL)
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the issue, including how an attacker might exploit it

### What to Expect

- Acknowledgment of your report within 48 hours
- Regular updates on our progress
- Credit in release notes (if desired) once the issue is resolved

## Preferred Languages

We prefer all communications to be in English.

## Security Best Practices for Users

As this is a client-side application with no backend:

1. **Always download from official sources**
   - GitHub repository: https://github.com/mariorazo97/quizmybrainz-wellness-tool
   - Official website: https://quizmybrainz.com

2. **Verify file integrity**
   - Check that index.html matches the repository version
   - Be cautious of third-party modifications

3. **Data Privacy**
   - This tool stores no data on servers
   - All assessment data remains in your browser session
   - No personal information is transmitted or stored

4. **Use HTTPS**
   - When deploying, always use HTTPS (GitHub Pages provides this automatically)
   - Never submit sensitive personal information through the tool

## Known Limitations

- This is an educational tool, not a clinical diagnostic instrument
- Results should not replace professional medical or psychological evaluation
- The tool is designed for general wellness assessment only

## Disclosure Policy

When we receive a security bug report, we will:

1. Confirm the issue and determine affected versions
2. Audit code to find similar issues
3. Prepare fixes for all supported versions
4. Release patches as soon as possible

Thank you for helping keep Body & Mind Detective and its users safe!
