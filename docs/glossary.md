# Glossary

**ADR** — Architecture Decision Record. A short document capturing one decision,
its context, and its consequences. Superseded ADRs are kept and marked.

**Charter** — the numbered list of rules in `01-context.md` that every change is
held against. A change that breaks a rule does not ship, regardless of who asked.

**Content vs. feature/design** — the central distinction of the system. Content
(posts, page copy, events) is data the editor owns and publishes instantly;
features and design are code the maintainer owns and promotes through
environments.

**CSS custom property** — a named, cascading CSS variable (`--color-ink`).
Components read these instead of literal colours or sizes, so swapping the values
restyles the whole site consistently.

**Design token** — a single named design value (a colour, a spacing step, a type
size). A preset is a complete, contrast-checked set of tokens.

**dev / uat / prod** — the three environments. `dev` is where a change is built,
`uat` is the editor's sign-off environment with realistic data, `prod` is the
public site. Same image, different configuration and data.

**Frontmatter** — the small block of structured metadata (title, date, tags,
cover image) at the top of a Markdown content file.

**GDPR** — the EU's General Data Protection Regulation. Governs every form field
and stored record: lawful basis, data minimalism, retention limits,
data-subject rights.

**Git mirror** — a git repository the API commits every content change to, with
the editor as author. It is an audit trail and a backup, **not** the publish
mechanism — publishing has already happened.

**Honeypot field** — a form field hidden from humans but visible to bots. A
submission that fills it in is discarded as spam.

**Hydration** — the SPA attaching interactivity to already-rendered static HTML
in the browser, so the first paint does not wait for JavaScript.

**Idempotent** — safe to run repeatedly with the same result. The blog importer
matches posts by slug, so it can be re-run to pick up anything published during
the migration.

**Lawful basis** — the GDPR justification for a given processing purpose
(e.g. consent or pre-contract for a contact form, contract for a booking).
Documented per purpose.

**Markdown** — the plain-text format the site's content is stored in. Portable,
diffable, greppable — not trapped in a database or a builder.

**MFA** — Multi-Factor Authentication. A second proof of identity beyond a
password, mandatory on the editor's account.

**Migration (database)** — a versioned, reversible schema change. Written to be
reversible so that a code rollback does not strand the data.

**ORM** — Object-Relational Mapper. The backend library that maps database rows
to code objects and manages schema migrations.

**Prerender** — rendering every public page and post to static HTML at deploy
time, served directly by the edge. The API is not on the critical path for
reading the site.

**`prefers-reduced-motion`** — a browser setting the site honours by suppressing
non-essential animation for visitors who ask for it. An accessibility
requirement.

**Preset** — a complete, designer-authored, contrast-validated set of design
tokens. The editor themes the site by choosing a preset — never a raw colour or
CSS field.

**Promotion** — moving a change forward by merging between environment branches
(`dev → uat → main`), each merge gated on CI and, for prod, the operator's
approval.

**Rate limit** — a cap on how often an endpoint (e.g. the contact form) will
accept requests from one source, to blunt spam and abuse.

**Rollback** — undoing a deploy with `git revert` and a redeploy of the
previous-good state. There are no hot edits to prod.

**RSS** — a machine-readable feed of blog posts so readers and aggregators can
subscribe.

**SEO** — Search Engine Optimisation. Here: correct metadata, a sitemap, clean
URLs, and prerendered content so the site is findable.

**Sitemap** — an XML file listing the site's URLs to help search engines
discover and index every page.

**Slug** — the URL-safe short name identifying a post (`/blog/<slug>`). Used as
the stable key when importing and updating content.

**SPA** — Single-Page Application. The JavaScript app that hydrates the
prerendered HTML and handles interactivity (tag filter, search).

**SSO** — Single Sign-On. The admin app and every future authenticated area
authenticate against one identity provider; local logins are disabled once SSO
is wired.

**VPN** — the private network path by which the operator reaches the admin app,
which is not exposed on the public edge in the target design.

**WAF** — Web Application Firewall. An edge filter that blocks common web
attacks before they reach the application.

**WCAG 2.2 AA** — the Web Content Accessibility Guidelines conformance level the
site must meet: contrast, keyboard operability, focus visibility, labelled
controls, alt text. Enforced in CI and in review.
