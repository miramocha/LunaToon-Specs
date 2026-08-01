---
title: Dual-pipeline shader assets
aliases: []
tags:
  - lunatoon
  - decision/shader
  - compatibility/birp
  - compatibility/urp
type: decision
status: accepted
---

# Dual-pipeline shader assets

## Status

Accepted.

## Context

LunaToon needs equal support for Unity Built-in Render Pipeline (BIRP) and
Universal Render Pipeline (URP). A single ShaderLab asset that targets both is
optional and often awkward: lighting includes, pass tags, and package
requirements differ.

Third-party megashaders that rely on ThryEditor, unlock-strip optimizers, or
huge `multi_compile` products create ship and Apply failures in related stacks
(see [shader authoring pitfalls](../references/shader-authoring-pitfalls.md)).
LunaToon will not use Thry.

Architecture previously left Shader Graph vs handwritten HLSL open. Dual-pipeline
sharing favors handwritten HLSL with shared includes.

## Decision

- The portable material and shading contract is **pipeline-agnostic** (property
  names, defaults, units, lighting behavior). Feature specs state BIRP and/or URP
  applicability when a rule is pipeline-specific.
- Unity implementations ship **sibling ShaderLab assets**: one public shader for
  BIRP and one for URP. Exact ShaderLab names are TBD when shaders land; names
  MUST differ per pipeline.
- Shared lighting and math live in `.hlsl` includes. Each pipeline wrapper owns
  lighting includes, pass structure, tags, and `#pragma` targets.
- A single dual-pipeline `.shader` is **not** required.
- Handwritten HLSL plus shared includes is the dual-pipeline sharing strategy.
  Shader Graph is an optional consumer of those includes (for example Custom
  Function nodes in File mode), not the primary dual-pipeline ship path.
- Shared `.hlsl` entrypoints intended for reuse SHOULD stay callable from Shader
  Graph Custom Function nodes: plain functions, no BIRP/URP-only includes in the
  Graph-facing file, and no dependence on ShaderLab pass state. Pipeline wrappers
  and Graph master stacks each supply their own lighting/bindings around that
  shared math.
- C# Editor or runtime scripts are not Shader Graph reuse units. Reuse across
  Graph and handwritten shaders is HLSL (and optional Sub Graphs), not C#.
- Do not ship ThryEditor or depend on unlock-strip build policy.
- Do not use optimizer lock copies (`Hidden/Locked/…`) as material identity.
- Material identity is the **public unlocked ShaderLab name** for the active
  pipeline.
- Keep `#pragma multi_compile` product small by design. Do not plan Always
  Included megashaders.
- Material inspectors use native Unity Editor code (`ShaderGUI` or equivalent) in
  the LunaToon code repo. Serialized properties are the contract; inspector
  chrome is not.

## Consequences

- [Architecture](../architecture.md) host map lists Unity BIRP and Unity URP as
  equal hosts.
- [Conformance](../specs/core/lunatoon-conformance.md) baseline covers both
  pipelines (BIRP pins TBD until measured).
- [LunaToon Unity](../implementations/lunatoon-unity.md) documents both pipelines
  in one host profile.
- Inspectors MUST NOT treat Thry-style `HideInInspector` toggle props as the
  portable contract.
- Authors can share one math include between BIRP/URP `.shader` wrappers and
  Shader Graph samples without making Graph the normative host path.
- Feature field tables remain out of scope until separate feature specs land.

## Related

- [Shader authoring pitfalls](../references/shader-authoring-pitfalls.md)
- [Separate specs vault](separate-specs-vault.md)
