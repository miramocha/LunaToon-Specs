---
title: LunaToon Rim
aliases: []
tags:
  - lunatoon
  - spec/features
  - compatibility/birp
  - compatibility/urp
type: specification
status: draft
---

# LunaToon Rim

Portable material and shading contract for LunaToon parametric rim light.
Skeleton draft: view-dependent rim and a lighting-mix control are in scope;
property identifiers, defaults, ranges, and exact formulas are mostly TBD.

## Scope

| Item | Value |
|------|-------|
| Feature | Parametric rim (N·V / fresnel family) |
| `specVersion` | `0.1.0` |
| Pipelines | BIRP and URP (equal hosts) |
| Material interchange | Unity materials only ([conformance](../core/lunatoon-conformance.md)) |
| Out of scope | Specular; matcap; screen-space outline; glTF / VRM packaging |

## Conformance

This specification conforms to [LunaToon Conformance](../core/lunatoon-conformance.md).

Specular and matcap belong in separate feature specs when drafted.

## Normative requirements

1. Hosts that implement this feature MUST compute a parametric rim from a
   view-dependent factor derived from surface normal and view direction
   (N·V fresnel family). Exact expression (power, lift, saturate order) is TBD.
2. Matcap-based edge glow MUST NOT be treated as a substitute for this feature’s
   contract.
3. Hosts MUST evaluate a scalar rim factor in `[0, 1]` (after published shaping)
   from normal and view.
4. Materials MUST expose controls that shape that factor. Skeleton roles: fresnel
   power and lift (or equivalent once named). Identifiers TBD.
5. Until identifiers are published, hosts MUST NOT treat ad-hoc Unity property
   names as normative.
6. When rim contribution is effectively zero (disabled or zero intensity; exact
   disable rule TBD), hosts MUST NOT add rim radiance from this feature.
7. Materials MUST expose a rim color factor (linear RGB; alpha role TBD).
8. Materials MAY expose a rim texture or mask that modulates rim color or
   intensity. UV set TBD.
9. When no rim texture is bound, hosts MUST treat modulation as `1` (or the
   published default once set).
10. Materials MUST expose a lighting mix factor in `[0, 1]` (identifier TBD).
    Semantics (MToon-inspired): `0` means constant (unlit-style) rim color;
    `1` means rim fully mixed with lighting; intermediate values blend between
    those ends. Exact lighting term (main light, GI, shadows) is TBD.
11. Hosts SHOULD keep rim appearance consistent across BIRP and URP for the same
    material field values, within engine lighting differences.
12. Whether rim is added to, multiplied into, or otherwise combined with the base
    toon shade result is TBD. Until published, hosts that ship rim MUST document
    the chosen composite in the implementation profile.

## Data model

Property identifiers below are placeholders. A later `specVersion` MUST replace
each `TBD` identifier before hosts treat names as normative.

| Role | Identifier | Type | Unit | Default | Range | Notes |
|------|------------|------|------|---------|-------|-------|
| Color factor | TBD | float3 or float4 | linear | TBD | TBD | Alpha role TBD |
| Fresnel power | TBD | float | — | TBD | TBD | Shapes N·V falloff |
| Lift | TBD | float | — | TBD | TBD | Or equivalent shape control |
| Lighting mix | TBD | float | — | TBD | `[0, 1]` | Constant vs lit rim |
| Rim texture / mask | TBD | texture2D | — | none | — | Optional |
| Rim UV | TBD | TBD | — | TBD | TBD | Open |
| Enable / intensity | TBD | TBD | — | TBD | TBD | Disable rule open |

## Compatibility

| Pipeline | Applicability |
|----------|---------------|
| URP | MUST apply when the host implements rim |
| BIRP | MUST apply when the host implements rim |

This feature does not raise baseline pins beyond
[conformance](../core/lunatoon-conformance.md). Hosts MUST state any extra Unity
or RP dependency in their implementation profile.

## Examples (non-normative)

Soft constant rim: low fresnel power, lighting mix `0`, pale color factor, no
rim texture.

Lit rim toward the key light: lighting mix `1`, higher power, color factor
matched to the look; exact light coupling still TBD in this draft.

## MToon mapping

Family rule: LunaToon SHOULD stay mappable to MToon, not one-to-one
([conformance](../core/lunatoon-conformance.md#normative-requirements)).
This feature’s parametric rim and lighting-mix roles follow that MToon-inspired
shape. LunaToon property names are not MToon ShaderLab identifiers and MUST NOT
be copied from `_RimColor`, `_RimFresnelPower`, `_RimLift`, `_RimLightingMix`,
or MToon10 equivalents.

### Role map (non-normative)

| LunaToon role | Familiar MToon idea |
|---------------|---------------------|
| Color factor | Parametric rim color |
| Fresnel power | Rim fresnel power |
| Lift | Rim lift |
| Lighting mix | Rim lighting mix factor |
| Rim texture / mask | Rim texture |

A converter MAY approximate when units, formulas, or packing differ.

## Open questions

- Exact rim formula (power, lift, saturate order).
- Main light vs ambient vs shadow dependence when lighting mix is above zero.
- Occlusion / toon shade masking of rim.
- Additive vs multiply (or other) composite with base shade and future specular.
- Default-off vs default-on; dedicated enable flag vs zero color/intensity.
- Energy interaction once shade and specular specs exist.

## Related

- [LunaToon Conformance](../core/lunatoon-conformance.md)
- [LunaToon Outline](outline.md)
- [Dual-pipeline shader assets](../../decisions/dual-pipeline-shader-assets.md)
- [LunaToon Unity](../../implementations/lunatoon-unity.md)
