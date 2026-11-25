# NEXORA research and partnership library

**Studio identity:** NEXORA Interactive Studios  
**Flagship product:** Nexora Foundry / NEXORA Studio Pro  
**Evidence snapshot:** 25 November 2026  
**Purpose:** Founder study, partner evaluation and technical due diligence.

NEXORA is treated as an independent creative-technology venture. Its studio charter states that it is operationally separate from RevelaCode. Shared authorship or technology work does not create an implied transfer of ownership, customer data, revenue, brand identity or legal affiliation.

## Reading order

1. [NEXORA partnership overview](PARTNERSHIP-OVERVIEW.md) — product proposition, target collaborators and partnership positioning.
2. [Partnership opportunities and pilot framework](PARTNERSHIP-OPPORTUNITIES.md) — practical work packages, potential partner roles and evaluation criteria.
3. [Windows desktop host architecture](WINDOWS-DESKTOP-HOST.md) — what this repository owns and how it builds the separate React workspace.
4. [LinkedIn partnership announcement](LINKEDIN-PARTNERSHIP-ANNOUNCEMENT.md) — public-facing draft.

## The three-repository boundary

| Repository | Responsibility |
|---|---|
| `musombi123/Nexora_Windows` | Tauri 2 Windows desktop host, Rust entry, installer configuration, desktop CI and host version |
| `musombi123/RevelaCode-Frontend/apps/nexora` | Independent NEXORA React/Vite application and creator-facing interface |
| `musombi123/Procedural-Game-Foundry` | Foundry API, project engine, procedural generation, Blender/Godot pipeline, asset registry, local compute agent, tests and technical product documentation |

The Windows host checks out the actual frontend workspace; it does not duplicate it. The Foundry engine and Local Agent are separate runtime components.

## Evidence and disclosure

This documentation is based on repository source and existing architecture/roadmap documents at the evidence date. It is not proof of a finished commercial release, live publisher integration, customer adoption, a signed installer or a tested performance guarantee.

Do not disclose private credentials, customer projects, personal photos, source media or unredacted local agent pairing details to a prospective partner. Use synthetic projects and controlled test environments.

## Related source repositories

- [NEXORA Windows host](https://github.com/musombi123/Nexora_Windows)
- [NEXORA React workspace](https://github.com/musombi123/RevelaCode-Frontend/tree/main/apps/nexora)
- [Procedural Game Foundry](https://github.com/musombi123/Procedural-Game-Foundry)
- [NEXORA Studio Charter](https://github.com/musombi123/Procedural-Game-Foundry/blob/main/docs/studio/NEXORA_STUDIO_CHARTER.md)
