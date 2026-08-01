---
title: Shader authoring pitfalls
aliases: []
tags:
  - lunatoon
  - type/reference
  - compatibility/birp
  - compatibility/urp
type: reference
status: draft
---

# Shader authoring pitfalls

Non-normative guidance for LunaToon shader authors. Normative rules live in
[conformance](../specs/core/lunatoon-conformance.md) and the
[dual-pipeline ADR](../decisions/dual-pipeline-shader-assets.md).

## Purpose

Capture shipping lessons from megashader and Thry-based stacks so LunaToon avoids
the same failure modes. This note is research and authoring advice, not a feature
contract.

## Do / don’t

| Topic | Do | Don’t |
|-------|----|-------|
| Asset split | Separate BIRP and URP ShaderLab entrypoints; share `.hlsl` includes | Require one dual-pipeline `.shader` for parity |
| Shader Graph reuse | Keep shared math in Graph-callable `.hlsl` (Custom Function File mode); optional Sub Graphs for Graph-only composition | Treat C# scripts as Graph reuse; put URP/BIRP Core lighting includes inside Graph-facing shared math |
| Names | Unique public ShaderLab name per pipeline | Register the same ShaderLab name under BIRP and URP packs |
| Keywords | Keep `#pragma multi_compile` product small; add axes only when needed | Poi-style effect `multi_compile` products that force Always Included or huge cook sets |
| Always Included | Ship shaders through normal package/load paths | Put LunaToon shaders on Always Included Shaders to “fix” variants |
| Thry | Native `ShaderGUI` / Editor code; unlocked public names as identity | ThryEditor, unlock-strip, or `Hidden/Locked/…` as Apply identity |
| Inspectors | Contract = serialized material properties | Treat UI folders, drawers, or `HideInInspector` chrome as the portable schema |
| URP packaging | Put `PackageRequirements` inside `SubShader` when required | Assume URP `Core.hlsl` exists on BIRP hosts; put `PackageRequirements` at Shader root |
| Warm / SVC | Prefer small keyword budgets so first-use hitch risk stays low | Plan unbounded `shader_feature` sets that need host-specific SVC warm to be usable |

## Keyword budget

Large effect toggles as `multi_compile` multiply fragment programs. Related
stacks cut axes hard and still measured tens of thousands of variants before
further trimming. LunaToon should start narrow: pipeline and quality axes only
when justified, feature toggles as `shader_feature` or material branches with a
deliberate budget.

If a future host cannot warm variants, missing keywords show up as stripped
passes or first-frame hitches. A small budget makes warm optional rather than
mandatory.

## Thry and lock copies

Thry unlock-strip can rename or remove public ShaderLab names. Lock copies under
`Hidden/Locked/…` are not stable Apply identities; some tools store
`OriginalShader` as a workaround. LunaToon does not use Thry, so materials and
overrides use the public unlocked name for the active pipeline only.

## Provenance (research)

Lessons distilled from VRMXT / Poiyomi shipping notes in
[Extended-VRM-Specs](https://github.com/miramocha/Extended-VRM-Specs). Those
docs are about Warudo/Player packs and admission gates; they are **not** LunaToon
normative text.

| Topic | Upstream note |
|-------|---------------|
| Variant / `multi_compile` product | [warudo-poiyomi-birp-variants](https://github.com/miramocha/Extended-VRM-Specs/blob/main/references/warudo-poiyomi-birp-variants.md) |
| Exclusions, ThryEditor strip from mods | [warudo-poiyomi-exclusions](https://github.com/miramocha/Extended-VRM-Specs/blob/main/references/warudo-poiyomi-exclusions.md) |
| Warm / load failure modes | [warudo-material-warmup](https://github.com/miramocha/Extended-VRM-Specs/blob/main/references/warudo-material-warmup.md) |
| Always Included, lock copies, pack policy | [vrmxt-player-shader-assetbundles](https://github.com/miramocha/Extended-VRM-Specs/blob/main/references/vrmxt-player-shader-assetbundles.md) |
| Admission gates (strip, keyword product) | [vrmxt-unity-shader-plugins](https://github.com/miramocha/Extended-VRM-Specs/blob/main/implementations/vrmxt-unity-shader-plugins.md) |

## Related

- [Dual-pipeline shader assets](../decisions/dual-pipeline-shader-assets.md)
- [LunaToon Architecture](../architecture.md)
- [LunaToon Unity](../implementations/lunatoon-unity.md)
