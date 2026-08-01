---
title: LunaToon Unity
aliases: []
tags:
  - lunatoon
  - implementation/unity
type: guide
status: draft
---

# LunaToon Unity

Host profile for the Unity implementation of LunaToon.

## Repository

| Field | Value |
|-------|-------|
| Repo | [miramocha/LunaToon](https://github.com/miramocha/LunaToon) |
| Role | Unity 6 URP host / sample project; future home for shaders and optional UPM package |
| Normative specs | [LunaToon-Specs](https://github.com/miramocha/LunaToon-Specs) |

## Measured pins

| Pin | Value | Source |
|-----|-------|--------|
| Unity Editor | `6000.3.7f1` | `ProjectSettings/ProjectVersion.txt` |
| URP | `17.3.0` | `Packages/packages-lock.json` |
| Pipeline assets | PC + Mobile URP renderers | `Assets/Settings/` |

## Current status

- Project is an URP Empty Template renamed to LunaToon.
- No custom shaders, materials package, or UPM `package.json` for LunaToon yet.
- Specs in this vault are ahead of implementation; hosts SHOULD treat feature docs as
  draft until the Unity repo implements them.

## Expected ownership (when shaders land)

| Concern | Location |
|---------|----------|
| Shaders / HLSL / Shader Graph | LunaToon (or nested UPM package) |
| Material inspectors / Editor tooling | LunaToon |
| Package SemVer / CHANGELOG | LunaToon |
| Portable property and behavior contracts | LunaToon-Specs |

## Capability matrix

| Area | Support | Notes |
|------|---------|-------|
| URP Forward | planned | Baseline pipeline |
| PC renderer asset | present | Template default |
| Mobile renderer asset | present | Template default |
| Outline | TBD | Feature spec not written |
| Cel shade / steps | TBD | Feature spec not written |
| Rim / specular / matcap | TBD | Feature spec not written |

## Related

- [Architecture](../architecture.md)
- [Conformance](../specs/core/lunatoon-conformance.md)
- [Separate specs vault](../decisions/separate-specs-vault.md)
