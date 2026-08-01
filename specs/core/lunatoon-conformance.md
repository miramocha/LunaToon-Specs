---
title: LunaToon Conformance
aliases: []
tags:
  - lunatoon
  - spec/core
  - spec/conformance
type: specification
status: draft
---

# LunaToon Conformance

Family-wide requirements for LunaToon specs and conforming implementations.
This document is not a single shading feature; feature contracts live under
[`specs/features/`](../features/).

## Purpose

Define shared rules so feature specs stay consistent and hosts know what
“conforming” means while the stack is still draft.

## Scope

| In scope | Out of scope |
|----------|--------------|
| Requirement strength, naming, `specVersion`, baseline host pins | Concrete outline/shade/rim field tables |
| How unknown properties and future features interact | Unity package layout, asmdefs, samples |
| Document placement for new normative notes | Third-party shader catalogs (lilToon, Poiyomi, …) |

## Requirement strength

Normative text MUST use:

| Keyword | Meaning |
|---------|---------|
| MUST | Absolute requirement for conformance |
| SHOULD | Strong recommendation; deviation needs a documented reason |
| MAY | Optional; hosts may omit |

Do not use soft marketing language in normative sections. Rationale and examples
MUST be labeled non-normative when mixed into a feature doc.

## Naming

- Spec filenames MUST use kebab-case (e.g. `lunatoon-conformance.md`).
- Feature specs MUST live under `specs/features/<feature>.md`.
- Material / shader property identifiers, once published in a feature spec, MUST
  stay stable or ship an explicit migration note.
- Until a feature spec publishes property names, hosts MUST NOT treat ad-hoc
  Unity property names as normative.

## `specVersion`

- Each normative feature or fragment that defines a data contract SHOULD declare
  a `specVersion` string.
- `specVersion` values describe **draft schema revisions**, not released product
  versions, unless a note explicitly states otherwise.
- Bumping `specVersion` for a breaking field change MUST include migration notes
  in that document (or a linked ADR).

## Baseline host (informative)

Primary development host pins (measured from [LunaToon](https://github.com/miramocha/LunaToon)):

| Pin | Value |
|-----|-------|
| Unity Editor | `6000.3.7f1` |
| URP | `17.3.0` |

Feature specs MAY require a higher pin. They MUST state compatibility when they
depend on a URP or Unity behavior beyond this baseline.

## Unknown and future features

- A conforming host SHOULD ignore unknown LunaToon properties it does not
  implement, unless a feature spec says otherwise.
- Adding a new feature MUST add a document under `specs/features/` and a row in
  the [README](../../README.md) Drafts table.

## Open questions

- Portable material interchange format (Unity materials only vs external schema) — TBD.
- Required vs optional feature matrix for “full” conformance — TBD.
