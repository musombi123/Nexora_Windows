# NEXORA Studio Pro — Windows desktop host architecture

**Evidence snapshot:** 25 November 2026  
**Repository:** `musombi123/Nexora_Windows`

## 1. Responsibility of this repository

This repository owns the NEXORA Windows desktop shell:

- Tauri 2 application configuration;
- Rust application entry point;
- Windows x64 installer target and NSIS settings;
- desktop build workflow;
- desktop application metadata and host versioning.

It does not own the creator-facing React workspace or the Foundry generation engine.

## 2. Source ownership and build flow

```text
Nexora_Windows repository
  +-- src-tauri/ (Tauri configuration + Rust host)
  +-- .github/workflows/nexora-windows.yml
  |
  +--> GitHub Actions checks out:
        RevelaCode-Frontend/apps/nexora
             |
             v
        independent NEXORA React/Vite build
             |
             v
        public/dev_nexora output
             |
             v
        Tauri packages this frontend
             |
             v
        Windows x64 NSIS installer artifact
```

The workflow records both desktop-host and frontend source revisions in a build manifest. This matters because a desktop installer combines two independently versioned repositories.

The Foundry API and paired Local Agent remain separate runtime components. The Tauri shell does not duplicate their backend or local compute responsibility.

## 3. Current configuration inspected

The checked-in Tauri v2 configuration declares:

- Product name: NEXORA Studio Pro.
- Tauri app version: 0.1.1.
- Identifier: `com.nexora.foundry`.
- A 1440 × 900 default window with minimum dimensions 960 × 640.
- NSIS as the Windows bundle target.
- Offline WebView installer mode and current-user installation mode.
- Frontend dev/build commands using the checked-out NEXORA workspace.

The host Rust entry uses Tauri's default builder and generated context. Most product behavior therefore remains in the React workspace and the Foundry/Local Agent services.

## 4. CI behavior

The workflow uses a Windows GitHub Actions runner. It checks out the host and NEXORA frontend source, sets up Node 22 and stable Rust with the Windows MSVC target, installs each repository's dependencies, builds the NEXORA Vite workspace, builds the Tauri host and uploads the NSIS installer and manifest.

A CI artifact means the workflow produced an installer file. It does not establish that the installer is code-signed, accepted by Microsoft Store, installed on a clean customer device or passed an end-user acceptance test.

## 5. Release gates

Before describing the Windows app as a production release, record:

- successful CI run and artifact checksum;
- paired frontend commit and host commit;
- clean Windows 10/11 install and first launch;
- Local Agent pairing and account verification;
- project creation, save, recovery and export;
- update/uninstall behavior and data preservation;
- Windows Defender/SmartScreen and signing policy;
- crash, error and rollback behavior;
- third-party licence notices.

The current workflow does not configure a paid signing service and does not claim Microsoft Store certification. The product should be described as a Windows desktop build path under validation until the acceptance gates are completed.

## 6. Versioning issue to reconcile

At the evidence snapshot, `src-tauri/tauri.conf.json` says version 0.1.1 while the host root `package.json` and Cargo package each declare 0.1.0. These are separate metadata locations and should be reconciled into a single release-version policy before publishing installers. Do not assume they are automatically synchronized.

## 7. Related implementation sources

- [NEXORA app in the frontend repository](https://github.com/musombi123/RevelaCode-Frontend/tree/main/apps/nexora)
- [Procedural Game Foundry engine](https://github.com/musombi123/Procedural-Game-Foundry)
- [NEXORA app README](https://github.com/musombi123/RevelaCode-Frontend/blob/main/apps/nexora/README.md)
- [NEXORA Windows workflow](../../.github/workflows/nexora-windows.yml)
