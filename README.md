# NEXORA Studio Pro — Windows

Standalone Windows desktop application powered by **Tauri 2**.

## Repository ownership

This repository owns the NEXORA desktop host: Tauri 2 configuration, Rust entry
point, Windows x64 NSIS packaging, desktop CI, and desktop versioning.

The actual NEXORA React workspace is maintained in
[`musombi123/RevelaCode-Frontend/apps/nexora`](https://github.com/musombi123/RevelaCode-Frontend/tree/main/apps/nexora).
The build checks out that source into `workspace/frontend`; it does not copy or
fork the frontend implementation into this repository.

Foundry runtime services and the Local Agent remain separate components. This
desktop host does not replace or duplicate their backend, project storage, or
local compute responsibilities.

## Build on Windows

Requirements: Windows 10/11, Node.js 22, Rust stable with the MSVC target,
and Microsoft C++ Build Tools.

Place the RevelaCode-Frontend repository at `workspace/frontend`, then install
its monorepo dependencies and the Tauri host dependencies:

```powershell
npm ci --prefix workspace/frontend
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

The `NEXORA Windows Tauri` workflow checks out both repositories, installs
the frontend monorepo dependencies from its root lockfile, builds the actual
NEXORA workspace, compiles the Tauri host, and uploads the Windows x64 NSIS
installer with a manifest recording both source commits.

A successful workflow artifact is a build output, not a signed Microsoft
Store package. The CI build does not require a paid signing service.
