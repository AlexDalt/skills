# Domain Docs

## Before exploring

This repo uses a single-context layout:

- Read `GLOSSARY.md` at the repo root.
- Read ADRs in `.agents/adr/` that touch the area being explored.

If either is absent, proceed silently. The `domain-modeling` skill
creates domain documentation lazily as terms or decisions are resolved.

## Use the glossary's vocabulary

Use the glossary's terms in issue titles, proposals, hypotheses,
and test names. Respect its explicitly avoided synonyms.

If a needed concept is missing, reconsider whether it belongs to
the domain or note the gap for `domain-modeling`.

## Flag ADR conflicts

If a proposal contradicts an existing ADR, surface the conflict
explicitly rather than silently overriding the decision.
