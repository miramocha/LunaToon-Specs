---
title: Separate specs vault
aliases: []
tags:
  - lunatoon
  - decision/repository
type: decision
status: accepted
---

# Separate specs vault

## Status

Accepted.

## Context

LunaToon needs durable shading and material contracts that can outlive a single
Unity project layout. The VRMXT stack already pairs a docs vault
([Extended-VRM-Specs](https://github.com/miramocha/Extended-VRM-Specs)) with a
Unity implementation ([UniVRMXT](https://github.com/miramocha/UniVRMXT)) using
GitHub links, not submodules.

LunaToon started as an empty Unity 6 URP host with no in-repo docs surface.

## Decision

- Keep normative specs, ADRs, and host profiles in **LunaToon-Specs**.
- Keep shaders, C#, samples, and package release notes in **LunaToon**.
- Cross-link with GitHub URLs from README / CONTRIBUTING / host profiles.
- Do not submodule LunaToon-Specs into the Unity project.

## Consequences

- Implementers read specs first; Unity diffs stay code-focused.
- Draft feature specs can land before shaders exist.
- Two remotes to maintain; registry tables in the specs README must stay current.
