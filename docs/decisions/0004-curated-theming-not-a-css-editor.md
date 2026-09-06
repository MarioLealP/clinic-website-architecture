# ADR 0004 · Curated presets, never a CSS or colour editor

**Status:** accepted

## Context

The editor wants the site to feel like the clinic's own and to be able to change
its look over time. The obvious way to grant that is a theme editor: colour
pickers, a font dropdown, maybe a custom-CSS box.

Every one of those is a way to produce an inaccessible, inconsistent, or broken
page — and the charter says an accessibility regression is a bug regardless of
who caused it.

## Decision

The only theming control is a **preset picker**. A preset is a named, complete
set of design tokens, authored and contrast-validated by a designer before it
ships. There is no colour picker, no font field, no custom CSS, and no access to
type scale or spacing.

## Consequences

**Good**

- The editor genuinely cannot create an illegible or off-brand page — the
  invalid states do not exist in the option set.
- Because components read tokens (never literals), a preset switch restyles the
  whole site coherently.
- Self-service theming becomes a safe future feature: it is just "set the active
  preset".

**Bad / accepted**

- New looks require a designer. The editor cannot invent a colour scheme at
  midnight. This is the point.
- The preset library has to be grown deliberately over time so "choice" stays
  real.

## Rejected alternatives

- **Full theme editor** — rejected: hands the editor every tool needed to break
  the charter.
- **Colour picker with a live contrast warning** — rejected: a warning is not a
  control; the broken state still ships if the editor clicks past it.
