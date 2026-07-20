# Changelog

All notable changes to **Proper 4K UI Project - CleanSlate Patch** are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.1.0] - 2026-07-20

Public release.

### Fixed
- Subscribing on Steam Workshop now shows the mod in the launcher.

## [1.0.3] - 2026-07-06

### Changed
- Inner `descriptor.mod` untracked and gitignored.

## [1.0.2] - 2026-07-06

### Fixed
- README CK2Plus compatibility recommends installing alongside the CK2Plus - Proper 4K UI Compatibility Submod, not as a replacement.
- Bug report template's CK2Plus mod-stack checkbox updated to match.

### Changed
- Bug report template's mod-version dropdown uses `v1.0.x (current)` instead of a per-release value.

## [1.0.1] - 2026-07-06

### Changed
- README Installation leads with the Steam Workshop subscribe link.
- README Community adds Steam Workshop Discussions and Paradox Forums links.

## [1.0.0] - 2026-07-06

First public release.

## [0.3.0] - 2026-07-06

### Added
- Added mod thumbnail.
- Added community files (CONTRIBUTING, SUPPORT, CODE_OF_CONDUCT, SECURITY, AGENTS, issue templates) and README Community section.

## [0.2.0] - 2026-07-06

### Added
- Upscaled `modifier_icons.dds` strip in CleanSlate's frame ordering, bundled from Proper 4K UI Project.
- Before/after modifier icon screenshots in `docs/` with thumbnails.

## [0.1.0] - 2026-07-05

### Added
- Project initialization — MIT `LICENSE`, `.gitignore`, `.gitattributes`, README, changelog.
- Mod descriptors — dependencies on CleanSlate + Proper 4K UI Project.
- Upscaled trait icons for 29 traits CleanSlate renames, bundled from Proper 4K UI Project.
  - `ukkos_hammer.dds` ships as insurance — currently unused because CleanSlate's sprite maps `GFX_trait_ukkos_hammer` to `ukkos_axe.dds`, kept in case that mapping is updated to link to CleanSlate's orphaned `ukkos_hammer.dds`.
- Before/after screenshots in `docs/` with thumbnails.
