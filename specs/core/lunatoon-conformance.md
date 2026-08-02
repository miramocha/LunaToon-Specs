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

Shared requirements for LunaToon feature specifications and conforming hosts.
Concrete feature specs cite this document and define their own property
contracts and `specVersion` values.

This document is not a shading feature. It adds no material properties by itself.

## Scope

| Item | Value |
|------|-------|
| Target | LunaToon material contracts on Unity hosts (BIRP and URP) |
| Applies to | Feature specs under `specs/features/` that cite this document |
| Material interchange | Unity materials only (`Material` / ShaderLab property values) |
| External schema | Out of scope for conformance (no glTF / standalone JSON material file) |
| Serialized family object | none |
| Baseline URP Editor | `6000.3.7f1` (from [LunaToon](https://github.com/miramocha/LunaToon)) |
| Baseline URP package | `17.3.0` |
| Baseline BIRP | TBD |

## Normative requirements

1. A conforming feature specification MUST live under `specs/features/<feature>.md`
   and MUST be listed in the [README](../../README.md) Drafts table.
2. Spec filenames MUST use kebab-case.
3. A feature specification that defines a data contract SHOULD declare a
   `specVersion` string. Values describe draft schema revisions, not released
   product versions, unless the note explicitly states otherwise.
4. Bumping `specVersion` for a breaking field change MUST include migration notes
   in that document or a linked ADR.
5. Material / shader property identifiers, once published in a feature spec, MUST
   stay stable or ship an explicit migration note.
6. Until a feature spec publishes property names, hosts MUST NOT treat ad-hoc
   Unity property names as normative.
7. A conforming host SHOULD ignore unknown LunaToon properties it does not
   implement, unless a feature spec says otherwise.
8. LunaToon material interchange MUST be Unity materials only: serialized Unity
   `Material` / ShaderLab property values on a conforming host shader. Hosts
   MUST NOT treat an external portable schema as part of LunaToon conformance.
9. An external interchange format MAY be added later by a dedicated note and a
   `specVersion` / migration story. Until then it is out of scope.
10. LunaToon shading features SHOULD stay mappable to MToon 1.0-style materials
    (VRM MToon / MToon10 capability shape): a host or tool SHOULD be able to
    translate LunaToon authored look into MToon parameters (and the reverse where
    the LunaToon feature set covers the MToon side) without inventing a second,
    incompatible outline/rim/shade model.
11. Mappability MUST NOT require a one-to-one property or unit match. LunaToon
    MAY use different identifiers, defaults, ranges, or packing. A mapping MAY be
    lossy (drop unsupported controls, clamp ranges, or supply documented defaults).
12. Feature specs MUST NOT treat MToon ShaderLab names as normative LunaToon IDs.
13. When a feature claims MToon-inspired shape, it SHOULD include a non-normative
    role mapping table for authors and converters.
14. Feature specs that depend on pipeline-specific behavior MUST state BIRP and/or
    URP applicability. BIRP and URP are equal target pipelines
    ([dual-pipeline ADR](../../decisions/dual-pipeline-shader-assets.md)).
15. Feature specs MAY require a higher host pin than the baseline in Scope. They
    MUST state compatibility when they depend on Unity or render-pipeline behavior
    beyond that baseline.
16. Exact MToon importer/exporter algorithms and VRM extension packaging are out
    of scope here until a dedicated interchange note exists.

## Capability support

Support is declared per feature, not for LunaToon as a whole.
A host claiming support for a feature MUST implement every normative requirement
in that feature specification (and any fragments it cites).

Partial support for a feature MUST be documented in the implementation profile.
It MUST NOT be presented as full support for that feature.

## Versioning

While these drafts remain experimental, citations to this document stay
unversioned. Feature specs still use their own `specVersion`.

Pinned conformance versions, and migration rules when those texts diverge, are
future work. They do not block experimental use of the family rules above.

## Related

- [LunaToon Outline](../features/outline.md)
- [LunaToon Rim](../features/rim.md)
- [Dual-pipeline shader assets](../../decisions/dual-pipeline-shader-assets.md)
- [LunaToon Unity](../../implementations/lunatoon-unity.md)
