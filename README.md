# Nexora Windows

Windows desktop packaging host for the existing Nexora Foundry application in [Procedural-Game-Foundry](https://github.com/musombi123/Procedural-Game-Foundry).

This repository owns the Windows Tauri 2 shell and its build artifacts. It does not fork the Foundry engine, duplicate its project database, or move creator projects to cloud storage.

## Build model

1. GitHub Actions checks out this repository and the Foundry source repository.
2. It installs the existing `apps/web` dependencies and builds the actual Nexora Foundry React/TypeScript workspace.
3. Tauri packages that production web bundle into a Windows x64 NSIS installer.
4. The workflow records the exact Foundry source commit and uploads the installer as a build artifact.

## Runtime boundary

The Foundry application is local-first. Its production compute engine and project data remain on the creator's Windows PC. The local agent is a separate process bound to `127.0.0.1:8765`; the hosted API is a control plane, not a project-build server.

**Delivery limitation:** this first Windows package is the desktop shell around the existing Foundry web workspace. It does not yet install or launch the Python Local Agent as a managed Windows service/sidecar. Pairing handoff and full PC acceptance must be completed before describing the installer as a self-contained production workstation.

## Build

The `Nexora Windows desktop` workflow runs on pushes to `main`, pull requests, and manual dispatch. The Windows x64 NSIS installer and source-revision manifest are retained as GitHub Actions artifacts.

## Development

Requirements: Node.js 22, Rust stable with the MSVC target, and Microsoft C++ Build Tools.

The workflow checks out Foundry under `workspace/foundry`, installs `workspace/foundry/apps/web`, and builds the Tauri host from this repository.
