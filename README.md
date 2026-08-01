---
title: LunaToon Specs
aliases: []
tags:
  - lunatoon
  - type/index
type: index
status: draft
---

# LunaToon Specs

Specifications and design notes for LunaToon, a URP toon shading stack.
This repository defines portable material and shading contracts.
Implementations live in separate code repositories.

Consumers:

| Repo | Role |
|------|------|
| [LunaToon](https://github.com/miramocha/LunaToon) | Unity 6 URP host / implementation project |

## Architecture

| Note | Topic | Status |
|------|-------|--------|
| [LunaToon Architecture](architecture.md) | Portable shading contract vs Unity URP implementation | draft |

## Decisions

| Note | Topic | Status |
|------|-------|--------|
| [Separate specs vault](decisions/separate-specs-vault.md) | Docs vault separate from Unity impl (VRMXT-style pair) | accepted |

## Drafts

| Note | Topic | Status |
|------|-------|--------|
| [LunaToon Conformance](specs/core/lunatoon-conformance.md) | Shared family requirements, naming, `specVersion` | draft |

Feature specs land under `specs/features/` (one file per shading capability).
Reusable fragments land under `specs/fragments/`.

## Implementation profiles

| Note | Target | Status |
|------|-------|--------|
| [LunaToon Unity](implementations/lunatoon-unity.md) | Unity 6 URP host (`6000.3.7f1`, URP `17.3.0`) | draft |

## References

Non-normative research notes belong under `references/`. None yet.

## Archive

Superseded drafts belong under `archive/`. None yet.
