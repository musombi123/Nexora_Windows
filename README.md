# NEXORA Studio Pro — Windows

Standalone Windows desktop application powered by **Tauri 2**.

## Repository ownership

This repository owns the NEXORA desktop host:

- Tauri 2 configuration and Rust application entry point
- Windows x64 NSIS installer packaging
- Desktop build and artifact workflow
- Desktop-specific versioning and release metadata

The actual NEXORA React workspace is maintained in
[`musombi123/RevelaCode-Frontend/apps/nexora`](https://github.com/musombi123/RevelaCode-Frontend/tree/main/apps/nexora).
The Windows build checks that source out into `workspace/frontend` and packages it;
it does not copy or fork the frontend implementation into this repository.

Foundry runtime services and the Local Agent remain separate components. This
desktop host does not replace, duplicate, or silently relocate their backend,
project storage, or local compute responsibilities.

## Build

Requirements: Windows 10/11, Node.js 22, Rust stable with the MSVC target,
and Microsoft C++ Build Tools.

Place the RevelaCode-Frontend repository at `workspace/frontend`, then run:

```powershell
npm ci --prefix workspace/frontend/apps/nexora
npm ci
npm run tauri:dev
```

To produce the installer:

```powershell
npm run tauri:build
```

The Tauri build invokes the NEXORA workspace production build and packages its
output into the desktop application.

## CI

The `NEXORA Windows Tauri` workflow checks out both repositories, builds the
actual NEXORA workspace, compiles the Tauri host, and uploads the Windows x64
NSIS installer with a manifest recording both source commits.

A successful workflow artifact is a build output; it is not a signed Microsoft
Store package. No paid signing service is required for this CI build.
