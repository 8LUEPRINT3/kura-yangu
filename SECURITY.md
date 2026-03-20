# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| Latest (main branch) | ✅ |

## Reporting a Vulnerability

**Please do NOT open a public GitHub Issue for security vulnerabilities.**

If you discover a security vulnerability in Kura Yangu, please report it privately:

1. **Email**: Open a private security advisory via GitHub → [Security Advisories](../../security/advisories/new)
2. **What to include**: Description of the vulnerability, steps to reproduce, potential impact, and any suggested fix.
3. **Response time**: We aim to acknowledge reports within 48 hours and resolve critical issues within 7 days.

## Security Design Principles

Kura Yangu is built with privacy as a core requirement:

- **Zero server-side location tracking** — all geolocation processing runs in the user's browser via the Haversine formula. GPS coordinates are never transmitted to any server.
- **No analytics** — no tracking pixels, no Google Analytics, no external telemetry.
- **No external scripts** — all JavaScript is embedded in the HTML. No CDN dependencies that could be compromised.
- **Static hosting** — GitHub Pages serves only static files. There is no backend, no database, no user accounts.
- **Input sanitization** — all dynamic content rendered into the DOM is HTML-escaped to prevent XSS.

## Known Limitations

- Security headers (HSTS, X-Frame-Options) cannot be set via meta tags on GitHub Pages. HTTPS is enforced by GitHub Pages by default.
- The `frame-ancestors` CSP directive is only effective as an HTTP header, not a meta tag.
