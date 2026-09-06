# ADR 0005 · The editor's own devices are untrusted

**Status:** accepted

## Context

The editor is the legitimate operator of the site's content. It is tempting to
extend trust to their devices — remember the session for a long time, skip MFA
on "their" laptop, allow a persistent API token on their phone — because it is
more convenient.

Their devices are ordinary consumer endpoints: a personal phone and a personal
laptop, shared context, no device management, whatever apps and browser
extensions accumulate on a personal machine over years.

## Decision

Treat the editor's endpoints as **outside the trust boundary**. They are a
trusted person; their devices are not trusted infrastructure.

- Sessions are short and re-authentication is routine.
- MFA is required every time a new session is established, on every device.
- No long-lived API tokens or credentials are issued to their devices.
- The admin app assumes its client may be compromised: server-side authorisation
  on every action, no security decision made in the browser, sensitive
  operations re-confirmed.
- The blast radius of one of their devices being compromised is bounded to "an
  attacker can do what the editor can do, for the length of one session" —
  never "an attacker has standing access".

## Consequences

**Good**

- A stolen phone or a malicious browser extension does not equal a persistent
  breach of the site.
- The security model does not depend on the least controllable part of the
  system (a personal device) being clean.

**Bad / accepted**

- The editor authenticates more often than a "trust this device" model would ask
  them to. The friction is deliberate and kept as low as MFA allows (WebAuthn /
  passkey rather than typing codes).
