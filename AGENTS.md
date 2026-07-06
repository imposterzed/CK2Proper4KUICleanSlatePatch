# Agent Guide

Quick orientation for AI coding agents (and humans) ramping up on this codebase. Read this before editing files.

## What this mod is

Crusader Kings II asset-overlay compatibility patch for the CleanSlate + Proper 4K UI Project stack. Two things Proper 4K UI Project doesn't cover under CleanSlate:

- **Renamed trait icons** — CleanSlate renames trait IDs (e.g. `fair` → `attractive`); Proper 4K UI Project's upscaled icons ship at the vanilla name. This patch bundles copies at the CleanSlate name.
- **Reindexed modifier icons** — CleanSlate rearranges the shared `modifier_icons.dds` sprite strip into good/bad pairs; Proper 4K UI Project's upscaled strip keeps vanilla ordering. This patch bundles an upscaled strip in CleanSlate's ordering.

No scripting, no decisions, no localisation.

The user-facing summary lives in `README.md`. Version history is in `CHANGELOG.md`.

## Critical gotchas — read these first

### 1. Load order matters

The `.mod` descriptors declare `dependencies = { "CleanSlate" "Proper4KUI" }`, so this mod loads *after* both. Its DDS files win the mod-stack overlay for `gfx/traits/*.dds` and `gfx/interface/modifier_icons.dds`. Verify load ordering via `logs/setup.log`.

### 2. Trait icons match CleanSlate names, with sprite-mapping exceptions

CleanSlate renames 32 vanilla trait IDs (e.g. `fair` → `attractive`, `robust` → `brawny`). This patch's trait icons live at `gfx/traits/<cleanslate_id>.dds`, sourced from Proper 4K UI Project's file at the *vanilla* name.

Exception: CleanSlate's `interface/traits.gfx` maps some `GFX_trait_<cs_id>` sprites to *vanilla*-named DDS (`ukkos_hammer` → `ukkos_axe.dds`). In those cases Proper 4K UI Project's original file wins directly and this patch's mirror at the CleanSlate name is dead weight — kept as insurance for future CleanSlate updates.

### 3. Modifier icon strip is a shared 134-frame sprite

`gfx/interface/modifier_icons.dds` is a single strip referenced by numeric `icon = N` in every event-modifier definition. Frame N in vanilla ≠ frame N in CleanSlate (CleanSlate reindexes to good/bad pairs). This patch ships the strip in CleanSlate's frame ordering, with Proper 4K UI Project's upscaled icons.

## Repo layout

```
Proper4KUICleanSlatePatch.mod                          top-level mod descriptor
Proper4KUICleanSlatePatch/                             mod content
  descriptor.mod                                        inner descriptor (mirror)
  thumbnail.png                                         mod thumbnail
  gfx/traits/*.dds                                      upscaled trait icons
  gfx/interface/modifier_icons.dds                      reordered modifier strip
docs/                                                   README screenshots + thumbnails
.github/ISSUE_TEMPLATE/                                 bug report + config
polish/                                                 untracked working area
CHANGELOG.md                                            version history (Keep a Changelog)
README.md                                               user-facing docs
```

## Testing

**There are no automated tests** — verification happens in-game only.

As an agent, you can:

- Verify DDS file dimensions and format via Pillow (`Image.open(...)`).
- Cross-check trait ID references against CleanSlate's `common/traits/`.
- Confirm which sprite mapping is in effect via CleanSlate's `interface/traits.gfx`.

You **cannot** verify visual rendering — upscaled quality, icon accuracy, or in-game placement — without in-game testing.

Console shortcuts for the maintainer:

- `charinfo` — enable character-ID tooltips.
- `add_trait <cs_id> <charID>` — visualize a trait icon.
- `add_modifier <modifier_id> <charID> -1` — visualize a modifier icon (permanent).

## Adding graphics

**Trait icons:** 43×43 uncompressed BGRA DDS. Source: Proper 4K UI Project's file at the *vanilla* name. Ship at `gfx/traits/<cleanslate_id>.dds`.

**Modifier icon strip:** 6700×50 DXT5 DDS (`gfx/interface/modifier_icons.dds`). Frames must be in CleanSlate's ordering. Regenerating from scratch:

1. Load vanilla + CleanSlate + Proper 4K UI Project `modifier_icons.dds` via Pillow.
2. Compute CS → vanilla frame mapping by pixel-diff nearest-neighbor (map is bijective; CleanSlate's reindex is a pure reordering).
3. Assemble an upscaled strip using Proper 4K UI Project's frames placed at CleanSlate's positions per the mapping.
4. Export as DDS in GIMP with BC3 / DXT5 compression (Pillow's DXT5 write is unreliable).

## Conventions

- **Commit messages:** subject `vX.Y.Z - <topic>` (~70 chars, no trailing period), topic is a noun phrase. Optional short body explaining the "why" — present tense.
- **Versioning:** semver, `0.x` range until first public release. Every commit tagged with `vX.Y.Z` (lightweight tag).
- **CHANGELOG:** [Keep a Changelog](https://keepachangelog.com/) format. Sub-sections in order: Added, Changed, Deprecated, Removed, Fixed, Security (omit empty ones). Entry ships in the SAME commit as the change.
- **Line endings:** `.md` / `.yml` = LF; `.mod` = CRLF (enforced by `.gitattributes`). DDS = binary, never text-processed.

## Things to avoid

- Modifying Proper 4K UI Project's original DDS files. Only ship copies under CleanSlate's names / ordering.
- Repainting icons. This patch is a *rearrangement* — always source pixels from the Proper 4K UI Project original, never redraw.
- Adding scripting, decisions, events, or localisation. This patch is asset-only by design.
- Adding a DDS for a trait ID CleanSlate doesn't rename. Only trait IDs CleanSlate actually reassigns need coverage — vanilla-named traits use Proper 4K UI Project's file directly via engine load-order.

## Resources

- **CK2 modding wiki:** https://ck2.paradoxwikis.com/Modding — reference for CK2 modding syntax.
- **CleanSlate:** https://github.com/ck2plus/CleanSlate — primary reference for CleanSlate's trait renames and modifier icon reindexing. Key files:
  - `master_changelog.txt` — trait-rename list.
  - `common/traits/*.txt` — trait definitions with `opposites` blocks.
  - `interface/traits.gfx` — sprite mappings (some redirect `GFX_trait_<cs_id>` to vanilla-named DDS).
  - `gfx/traits/*.dds` — CleanSlate's shipped standard resolution icons.
  - `gfx/interface/modifier_icons.dds` — CleanSlate's reindexed modifier strip.
- **Proper 4K UI Project source** at `Documents/Paradox Interactive/Crusader Kings II/mod/Proper4KUI/` — upscaled source assets. Key folders:
  - `gfx/traits/*.dds` — upscaled trait icons at vanilla names.
  - `gfx/interface/modifier_icons.dds` — upscaled modifier strip in vanilla ordering.
- **Vanilla CK2 install** — reference for baseline sprite definitions. Common locations:
  - Steam: `C:/Program Files (x86)/Steam/steamapps/common/Crusader Kings II/`
  - GOG Galaxy: `C:/Program Files (x86)/GOG Galaxy/Games/Crusader Kings II/`

  Key files:
  - `gfx/traits/*.dds` — trait icons.
  - `gfx/interface/modifier_icons.dds` — modifier strip.
  - `common/traits/*.txt` — trait definitions.
  - `common/event_modifiers/*.txt` — modifier definitions.
  - `interface/province.gfx` — modifier sprite registration.
