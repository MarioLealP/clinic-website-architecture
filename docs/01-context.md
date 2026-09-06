# 1 · Context

## Who this is for

A small clinic with one person responsible for keeping the website current. They
are the sole author and the sole editor. There is no marketing team, no
webmaster, and no appetite for either.

Their interaction with the system is entirely conversational: they say "add a
post about X", "the homepage text should say Y", "this looks good" — and the site
changes. They never see a repository, a build, a deploy, or a config file.

## Constraints

- **The clinic's primary language is not English** — content, UI, dates, and
  number formatting all follow the local language and conventions.
- **An established blog** — roughly 180 existing posts to migrate off a hosted
  website builder, with their publication dates, cover images, and tags intact.
  The author's words, verbatim — no rewriting.
- **Accessibility is a requirement, not a target.** WCAG 2.2 AA is the floor.
- **The clinic is in the EU** — data-protection law applies to every form and
  every stored field.
- **Small budget, single operator.** The running cost and the operational load
  both have to stay near zero.

## Charter

These rules govern every change. A change that breaks one does not ship,
regardless of who asked for it.

1. **Accessibility first.** Semantic HTML, full keyboard use, visible focus,
   contrast ≥ 4.5:1, labelled forms, alt text, a correct `lang` attribute,
   honours `prefers-reduced-motion`. A regression here is a bug.
2. **Security first.** No secrets in the repo. Behind a WAF. Authenticated areas
   are SSO-only. Server-side validation on every input. Forms carry a honeypot
   and a rate limit. Dependencies are pinned and aged before adoption.
3. **The design system is the guardrail.** The editor customises by choosing
   from designer-approved presets, never a free-form colour or CSS field. They
   cannot reach a setting that breaks layout, rhythm, or contrast.
4. **The assistant is an editor, not a stenographer.** When a request would hurt
   clarity, consistency, accessibility, performance, SEO, or brand, the
   tradeoff is named and an intent-preserving alternative offered first.
5. **Consistency everywhere.** One nav, one footer, one type scale, one spacing
   rhythm, one voice. Pages differ in content, not mechanics.
6. **Reviewable by default.** Every change to features or design is a diff,
   promoted through environments. Content changes are not gated (see
   `03-content-pipeline.md`) but are still captured as an audit trail.
7. **Performance and SEO are features.** Fast first paint, prerendered content,
   correct metadata, sitemap, RSS.
8. **Data minimalism.** Collect only what a contact or a booking needs. Privacy
   notice, lawful basis, retention policy, no third-party trackers.
9. **Reversibility.** Everything version-controlled, migrations reversible,
   backups cover the data, every deploy can roll back.
10. **Scope discipline.** v1 is the public site and blog. The members-only area
    and booking are separate phases with their own designs.

## Phasing

| Phase | Scope | Status in this document |
| --- | --- | --- |
| 1 | Public site + blog, content pipeline | the subject |
| 2 | Members-only area — auth-gated material | designed for, not built |
| 3 | In-browser authoring for the editor (no assistant in the loop) | designed for |
| 4 | Online booking for appointments | designed for |

Phases 2 and 4 are the reason the architecture has a real backend from day one
(ADR 0001).
