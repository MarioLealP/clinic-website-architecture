# ADR 0002 · Content lives in git, but is authored in prod

**Status:** accepted · supersedes the original "all changes are promoted through
environments" rule for content

## Context

The first design treated *everything* as a reviewable change promoted
`dev → uat → prod`, including blog posts. That is correct for code. For content
it means the editor writes a post, then waits for a maintainer to promote it
through two environments before the world can read it. For someone who publishes
several times a week, that is unworkable — and it makes the maintainer a
bottleneck on the editor's own words.

## Decision

Split the two:

- **Features and design** — promoted through environments, CI-gated,
  operator-approved. Unchanged.
- **Blog posts, events, and page copy** — authored in the live admin app and
  published immediately, no deploy. Every such change is still committed to a
  **git mirror** by the system, as an audit trail and backup, not as a gate.

## Consequences

**Good**

- The editor is autonomous for the thing they do most.
- No deploy pipeline runs for a typo fix.
- History and restore-any-version are preserved via the mirror.

**Bad / accepted**

- "Publish" is now a real action with no human review step — so the authoring
  path itself must enforce the charter (accessibility, voice, safe content
  subset). The guardrails move from the pipeline into the editor.
- Two mental models for "how a change goes live". The `03-content-pipeline.md`
  table is the reference.

## Rejected alternatives

- **Keep promoting content through environments** — rejected: makes the
  maintainer a bottleneck on the editor's core workflow.
- **Content in a database, no git** — rejected: loses the portable, diffable,
  restorable history that makes instant publishing safe to allow.
