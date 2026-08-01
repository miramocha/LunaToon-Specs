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

Specifications and design notes for LunaToon, a toon shading stack with equal
Unity BIRP and URP hosts.
This repository defines portable material and shading contracts.
Implementations live in separate code repositories.

Consumers:

| Repo | Role |
|------|------|
| [LunaToon](https://github.com/miramocha/LunaToon) | Unity host / implementation project (BIRP + URP) |

## Architecture

| Note | Topic | Status |
|------|-------|--------|
| [LunaToon Architecture](architecture.md) | Portable shading contract vs Unity BIRP/URP implementation | draft |

## Decisions

| Note | Topic | Status |
|------|-------|--------|
| [Separate specs vault](decisions/separate-specs-vault.md) | Docs vault separate from Unity impl (VRMXT-style pair) | accepted |
| [Dual-pipeline shader assets](decisions/dual-pipeline-shader-assets.md) | Equal BIRP/URP via sibling shaders and shared HLSL; no Thry | accepted |

## Drafts

| Note | Topic | Status |
|------|-------|--------|
| [LunaToon Conformance](specs/core/lunatoon-conformance.md) | Shared family requirements, naming, `specVersion` | draft |

Feature specs land under `specs/features/` (one file per shading capability).
Reusable fragments land under `specs/fragments/`.

## Implementation profiles

| Note | Target | Status |
|------|-------|--------|
| [LunaToon Unity](implementations/lunatoon-unity.md) | Unity BIRP + URP hosts (URP pins `6000.3.7f1` / `17.3.0`; BIRP TBD) | draft |

## References

| Note | Topic | Status |
|------|-------|--------|
| [Shader authoring pitfalls](references/shader-authoring-pitfalls.md) | Dual-pipeline and Thry/megashader anti-patterns (non-normative) | draft |

## Archive

Superseded drafts belong under `archive/`. None yet.
