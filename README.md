# fly-narwhal-libmpv

Self-hosted libmpv archive mirror for [FlyNarwhal](https://github.com/FNOSP/FlyNarwhal) Windows desktop builds.

## Purpose

Upstream daily builds (zhongfly/mpv-winbuild, shinchiro/mpv-winbuild-cmake) only keep the last ~30 days of releases. To avoid build failures caused by deleted assets, this repository hosts the exact libmpv archives that FlyNarwhal pins.

## How FlyNarwhal fetches the archives

The Flutter/CMake build downloads the **latest release** from this repository:

- x86_64: `https://github.com/Jankin-Wu/fly-narwhal-libmpv/releases/latest/download/mpv-dev-x86_64.7z`
- aarch64: `https://github.com/Jankin-Wu/fly-narwhal-libmpv/releases/latest/download/mpv-dev-aarch64.7z`

The matching SHA256 checksums are stored in [`mpv-sha256.txt`](./mpv-sha256.txt) in the repository root. The build script downloads this file first and verifies the archive against it.

## Current status

- Repository created and populated with x86_64 + aarch64 archives.
- Tag `v2026.05.31` pushed and release auto-published via GitHub Actions.
- Release assets are available at `https://github.com/Jankin-Wu/fly-narwhal-libmpv/releases/latest/download/...`

## How releases are published

The repository includes a GitHub Actions workflow (`.github/workflows/release.yml`) that automatically creates a release and uploads the archives whenever a tag matching `v*` is pushed.

To publish a new version:

1. Replace `mpv-dev-x86_64.7z` and/or `mpv-dev-aarch64.7z` with the new archives.
2. Update `mpv-sha256.txt` with the new SHA256 values.
3. Commit and push the changes.
4. Push a new tag matching `v*` (for example: `git tag v2026.06.01 && git push origin v2026.06.01`).
5. GitHub Actions will create the release and upload the assets automatically.

## Current archives

| Architecture | Source archive | Commit | SHA256 |
|---|---|---|---|
| x86_64  | shinchiro/mpv-winbuild-cmake `20260531` | `13a3e3a` | `3e963f0c8dfd7273470e65fbe34b47dd745bcfaf21cb20ced4ed6a502f392a7b` |
| aarch64 | shinchiro/mpv-winbuild-cmake `20260531` | `13a3e3a` | `64ad76064c4ca26377334746f2897570cea9ad0426a8782d130b2f0485f68fdd` |

> Note: The originally intended `mpv-dev-x86_64-20260706-git-c8c7d91a8e` (zhongfly build) could not be located online because zhongfly only retains releases for ~30 days. The 2026-05-31 shinchiro build is used as the initial version while keeping the same archive layout and is verified to work with FlyNarwhal's full libmpv setup.
