# fly-narwhal-libmpv

Self-hosted libmpv archive mirror for [FlyNarwhal](https://github.com/FNOSP/FlyNarwhal) Windows desktop builds.

## Purpose

Upstream daily builds (zhongfly/mpv-winbuild, shinchiro/mpv-winbuild-cmake) only keep the last ~30 days of releases. To avoid build failures caused by deleted assets, this repository hosts the exact libmpv archives that FlyNarwhal pins.

## How FlyNarwhal fetches the archives

The Flutter/CMake build downloads the **latest release** from this repository:

- x86_64: `https://github.com/Jankin-Wu/fly-narwhal-libmpv/releases/latest/download/mpv-dev-x86_64.7z`
- aarch64: `https://github.com/Jankin-Wu/fly-narwhal-libmpv/releases/latest/download/mpv-dev-aarch64.7z`

The matching SHA256 checksums are stored in [`mpv-sha256.txt`](./mpv-sha256.txt) in the repository root. The build script downloads this file first and verifies the archive against it.

## How to publish a new libmpv version

1. Obtain the verified libmpv archive(s) for the desired date/architecture.
2. Rename the assets to the fixed names:
   - `mpv-dev-x86_64.7z`
   - `mpv-dev-aarch64.7z`
3. Create a new GitHub Release in this repository.
4. Upload the renamed archive(s) to the release.
5. Update `mpv-sha256.txt` in this repository with the SHA256 of each uploaded archive, in the format:

   ```text
   x86_64  <sha256>
   aarch64 <sha256>
   ```

6. Commit and push the updated `mpv-sha256.txt`.

After pushing the new checksum, FlyNarwhal builds will automatically pick up the new release.

## Current archives

| Architecture | Source archive | Commit | SHA256 |
|---|---|---|---|
| x86_64  | shinchiro/mpv-winbuild-cmake `20260531` | `13a3e3a` | `3e963f0c8dfd7273470e65fbe34b47dd745bcfaf21cb20ced4ed6a502f392a7b` |
| aarch64 | shinchiro/mpv-winbuild-cmake `20260531` | `13a3e3a` | `64ad76064c4ca26377334746f2897570cea9ad0426a8782d130b2f0485f68fdd` |

> Note: The originally intended `mpv-dev-x86_64-20260706-git-c8c7d91a8e` (zhongfly build) could not be located online because zhongfly only retains releases for ~30 days. The 2026-05-31 shinchiro build is used as the initial version while keeping the same archive layout and is verified to work with FlyNarwhal's full libmpv setup.
