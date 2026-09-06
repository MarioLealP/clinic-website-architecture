# ADR 0001 · A real backend from day one

**Status:** accepted

## Context

v1 is a public marketing site and a blog. That is a textbook static-site
job — a static generator would prerender it, a CDN would serve it, and there
would be no server to run or patch.

But the known roadmap includes a contact form with server-side handling, an
auth-gated private area (phase 2), in-browser authoring for the editor
(phase 3), and an online booking system (phase 4). Every one of those needs a
server that holds state and enforces rules.

## Decision

Ship a real backend (a typed web framework with an ORM and migrations) in v1,
even though v1 barely uses it. Design the data model and the API for phases 2–4
now. Keep the public site prerendered and served from the edge regardless, so
the backend is not on the read path.

## Consequences

**Good**

- The data model is designed once, not reverse-engineered later under pressure.
- The contact form is handled properly in v1 — validated server-side, stored,
  spam-defended — with no third-party form service.
- Phases 2–4 are additions, not rewrites.

**Bad / accepted**

- There is a server to run, monitor, and keep patched from day one.
- v1 carries a small amount of code it does not strictly need yet.

## Rejected alternative

- **Static site now, backend when phase 2 arrives** — rejected: guarantees
  designing the content/data model twice and a disruptive migration exactly when
  the first paying feature (the private area) is being built.
