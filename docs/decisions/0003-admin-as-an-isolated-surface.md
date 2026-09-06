# ADR 0003 · The admin app is an isolated surface, not a gated route

**Status:** accepted

## Context

The admin app can publish content, change settings, and (later) read personal
data and booking records. The convenient pattern is to serve it at
`/admin` on the public site, or at `admin.<domain>`, behind the same SSO as
everything else.

## Decision

The admin app is a **separate service** with its own deployable, its own data
access, and its own network placement. It is not a route on the public app. In
the target design it is reachable only through the operator's VPN, or — where a
web-reachable admin is genuinely needed — through a dedicated, tightly scoped
SSO route that shares nothing with the public site's routing.

## Consequences

**Good**

- A vulnerability in the public site (XSS, a routing bug, a dependency CVE)
  cannot reach admin functionality — different origin, different service,
  different network.
- The admin app can be locked down harder than a public site can (stricter CSP,
  no public caching, aggressive session policy) without compromising the public
  experience.
- The public site's attack surface does not include "the publish API".

**Bad / accepted**

- Two apps to build and deploy instead of one.
- The editor reaches admin via a slightly less convenient path than a bookmark
  to `/admin` would be.

## Rejected alternatives

- **`/admin` on the public app behind SSO** — rejected: shares an origin and a
  codebase with the most-attacked surface on the platform.
- **`admin.<domain>` behind SSO, same infra** — better, but still a public
  endpoint whose safety depends entirely on the SSO layer being flawless.
