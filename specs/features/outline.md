---
title: LunaToon Outline
aliases: []
tags:
  - lunatoon
  - spec/features
  - compatibility/birp
  - compatibility/urp
type: specification
status: draft
---

# LunaToon Outline

Portable material and shading contract for LunaToon mesh outlines.
Skeleton draft: technique and width-mode semantics are locked; property
identifiers, defaults, and ranges are mostly TBD.

## Scope

| Item | Value |
|------|-------|
| Feature | Outline (inverted-hull) |
| `specVersion` | `0.1.0` |
| Pipelines | BIRP and URP (equal hosts) |
| Material interchange | Unity materials only ([conformance](../core/lunatoon-conformance.md)) |
| Out of scope | Screen-space / post-process outlines; specular; matcap; cel shade; glTF / VRM packaging |

## Conformance

This specification conforms to [LunaToon Conformance](../core/lunatoon-conformance.md).

## Normative requirements

1. Hosts that implement this feature MUST use an inverted-hull outline: extrude
   back-facing geometry to form a silhouette stroke. Screen-space edge detection
   and other outline techniques are out of scope unless a later ADR adopts them.
2. Pipeline-specific pass wiring (extra ShaderLab pass or renderer feature) is a
   host concern
   ([dual-pipeline ADR](../../decisions/dual-pipeline-shader-assets.md)).
   The portable contract is the material fields and width/color behavior here.
3. Outline width mode MUST be one of: `none` (disabled; hosts SHOULD skip outline
   work), `world` (world-space width; unit TBD), `screen` (screen-relative width;
   unit TBD). Stable enum / property identifiers are TBD.
4. Until identifiers are published, hosts MUST NOT treat ad-hoc Unity property
   names as normative.
5. When mode is `none`, color and width textures MUST have no visible outline
   effect.
6. Materials MUST expose an outline color factor (linear RGB; alpha role TBD).
7. Materials MAY expose a width or mask texture that scales or gates outline
   width. Sampling UV set is TBD.
8. When no width/mask texture is bound, hosts MUST treat width scale as `1` (or
   the published default once set).
9. Hosts SHOULD keep outline appearance consistent across BIRP and URP for the
   same material field values, within engine lighting differences.
10. Exact cull face, Z-write, Z-bias, lit vs unlit outline, and alpha clip /
    transparent interaction are TBD (see [Open questions](#open-questions)).

## Data model

Property identifiers below are placeholders. A later `specVersion` MUST replace
each `TBD` identifier before hosts treat names as normative.

| Role | Identifier | Type | Unit | Default | Range | Notes |
|------|------------|------|------|---------|-------|-------|
| Width mode | TBD | enum | — | TBD (`none` expected) | `none` \| `world` \| `screen` | Semantics above |
| Width factor | TBD | float | TBD per mode | TBD | TBD | Scaled by width/mask map when present |
| Color factor | TBD | float3 or float4 | linear | TBD | TBD | Alpha role TBD |
| Width/mask texture | TBD | texture2D | — | none | — | Optional |
| Width/mask UV | TBD | TBD | — | TBD | TBD | Open |

## Compatibility

| Pipeline | Applicability |
|----------|---------------|
| URP | MUST apply when the host implements outline |
| BIRP | MUST apply when the host implements outline |

This feature does not raise baseline pins beyond
[conformance](../core/lunatoon-conformance.md). Hosts MUST state any extra Unity
or RP dependency in their implementation profile.

## Examples (non-normative)

World-width outline with solid color, no mask: set width mode to `world`, set
width factor and color factor, leave width/mask texture unbound.

Disabled outline: width mode `none`. Remaining outline fields may stay authored
for later re-enable; they MUST NOT affect shading while mode is `none`.

## MToon mapping

Family rule: LunaToon SHOULD stay mappable to MToon, not one-to-one
([conformance](../core/lunatoon-conformance.md#normative-requirements)).
This feature’s width-mode and color roles follow that MToon-inspired shape.
LunaToon property names are not MToon ShaderLab identifiers and MUST NOT be
copied from `_OutlineWidth`, `_OutlineColor`, or MToon10 equivalents.

### Role map (non-normative)

| LunaToon role | Familiar MToon idea |
|---------------|---------------------|
| Width mode | Outline width mode (none / world / screen) |
| Width factor | Outline width |
| Color factor | Outline color |
| Width/mask texture | Outline width multiply texture |

A converter MAY approximate when units or packing differ.

## Open questions

- Z-bias / depth offset for hull vs base mesh.
- Lit vs unlit outline surface; if lit, which lights.
- Screen-mode width units (pixels vs NDC-derived scale).
- Mask UV channel and whether color is textured separately from width.
- Alpha clip and transparent queue interaction with the outline pass.
- Default width mode and numeric defaults once identifiers land.

## Related

- [LunaToon Conformance](../core/lunatoon-conformance.md)
- [LunaToon Rim](rim.md)
- [Dual-pipeline shader assets](../../decisions/dual-pipeline-shader-assets.md)
- [LunaToon Unity](../../implementations/lunatoon-unity.md)
