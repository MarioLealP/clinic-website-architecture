# 5 · Security and Privacy

## Threat model

| Asset | Threat | Mitigation |
| --- | --- | --- |
| Public site availability | DoS, bad deploy | Prerendered content served from the edge; site reads even if the API is down; every deploy reversible |
| Contact-form endpoint | Spam, abuse, injection | Honeypot field, rate limit, server-side validation, stored as data (not emailed as raw input) |
| Editor's account | Phishing, credential theft, device compromise | SSO with mandatory MFA; the editor's own devices are treated as **untrusted** (ADR 0005) |
| Admin app | Direct exposure, session theft | SSO-only, no local login; not on the public edge in the target design — reached via the operator's VPN or a tightly scoped SSO route |
| Content integrity | Accidental or malicious edit | Every change mirrored to git with history; any version restorable |
| Stored personal data | Over-collection, breach, retention creep | Data minimalism, documented lawful basis, retention limits, encryption at rest via backups |
| Supply chain | Compromised dependency | Pinned versions, minimum release age before adoption, no auto-merge |

## Hardening baseline

- **Edge**: TLS everywhere, HSTS, a web application firewall, security headers
  (CSP, `X-Content-Type-Options`, `Referrer-Policy`, frame denial).
- **App**: runs as non-root, minimal image, no Docker socket, read-only where
  possible, secrets injected at runtime from an encrypted store — never in the
  repo or the image.
- **Input**: validated server-side on every endpoint. The client's validation is
  a convenience, not a control.
- **Auth**: authenticated areas are SSO-only. Local logins are disabled once SSO
  is wired, so there is no MFA-bypassing side door.

## Privacy (GDPR)

The clinic is in the EU; the site collects personal data through its contact
form and, later, its booking flow.

- **Collect the minimum.** A contact needs a name, a way to reply, and a
  message. Nothing else is asked for.
- **Lawful basis is documented** per processing purpose (contact = consent /
  pre-contract; booking = contract).
- **Retention is bounded.** Contact messages and booking records have a defined
  lifetime and are purged after it.
- **No third-party trackers.** No analytics that phone home without consent; no
  embedded widgets that set cookies. If usage measurement is added, it is
  privacy-preserving and consented.
- **A privacy notice** in the clinic's language explains what is collected, why,
  for how long, and how to exercise data-subject rights.

## Accessibility as a security-adjacent guarantee

WCAG 2.2 AA is enforced in CI (automated checks) and in review (manual keyboard
and screen-reader passes). It is in this document because, like the items above,
it is a property the system must *not* regress — a broken focus order or an
unlabelled form is treated as a defect of the same class as a missing security
header.
