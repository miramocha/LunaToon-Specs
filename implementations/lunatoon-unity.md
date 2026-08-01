---
title: LunaToon Unity
aliases: []
tags:
  - lunatoon
  - implementation/unity
  - compatibility/birp
  - compatibility/urp
type: guide
status: draft
---

# LunaToon Unity

Host profile for the Unity implementation of LunaToon. BIRP and URP are equal
targets in one repo until a package split is decided
([dual-pipeline ADR](../decisions/dual-pipeline-shader-assets.md)).

## Repository

| Field | Value |
|-------|-------|
| Repo | [miramocha/LunaToon](https://github.com/miramocha/LunaToon) |
| Role | Unity host / sample project; future home for sibling BIRP and URP shaders and optional UPM package |
| Normative specs | [LunaToon-Specs](https://github.com/miramocha/LunaToon-Specs) |

## URP

### Measured pins

| Pin | Value | Source |
|-----|-------|--------|
| Unity Editor | `6000.3.7f1` | `ProjectSettings/ProjectVersion.txt` |
| URP | `17.3.0` | `Packages/packages-lock.json` |
| Pipeline assets | PC + Mobile URP renderers | `Assets/Settings/` |

### Current status

- Project is an URP Empty Template renamed to LunaToon.
- No custom shaders, materials package, or UPM `package.json` for LunaToon yet.
- Specs in this vault are ahead of implementation; hosts SHOULD treat feature docs as
  draft until the Unity repo implements them.

## BIRP

### Measured pins

| Pin | Value | Source |
|-----|-------|--------|
| Unity Editor | TBD | Not measured yet |
| Built-in RP | TBD | Not measured yet |
| Pipeline assets | TBD | Not present yet |

### Current status

- Equal host target with URP; sibling ShaderLab asset plus shared HLSL includes
  when shaders land.
- No BIRP sample project settings or shaders in LunaToon yet.
- Do not invent BIRP version pins until a BIRP host configuration exists and is
  measured.

## Expected ownership (when shaders land)

| Concern | Location |
|---------|----------|
| BIRP ShaderLab entrypoint | LunaToon (or nested UPM package) |
| URP ShaderLab entrypoint | LunaToon (or nested UPM package) |
| Shared HLSL includes | LunaToon (or nested UPM package) |
| Material inspectors / Editor tooling | LunaToon (native Unity Editor; no Thry) |
| Package SemVer / CHANGELOG | LunaToon |
| Portable property and behavior contracts | LunaToon-Specs |

## Capability matrix

| Area | Support | Notes |
|------|---------|-------|
| URP Forward | planned | Equal baseline pipeline |
| BIRP Forward | planned | Equal baseline pipeline; pins TBD |
| PC URP renderer asset | present | Template default |
| Mobile URP renderer asset | present | Template default |
| Outline | TBD | Feature spec not written |
| Cel shade / steps | TBD | Feature spec not written |
| Rim / specular / matcap | TBD | Feature spec not written |

## Related

- [Architecture](../architecture.md)
- [Conformance](../specs/core/lunatoon-conformance.md)
- [Dual-pipeline shader assets](../decisions/dual-pipeline-shader-assets.md)
- [Shader authoring pitfalls](../references/shader-authoring-pitfalls.md)
- [Separate specs vault](../decisions/separate-specs-vault.md)
