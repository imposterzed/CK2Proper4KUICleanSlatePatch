# Contributing to Proper 4K UI Project - CleanSlate Patch

Thanks for your interest in contributing! This document covers bug
reports and code contributions.

- For what the mod does, see the [README](README.md).
- For the technical ramp-up (repo layout, DDS handling, PIL / GIMP
  workflow, commit conventions), see [AGENTS.md](AGENTS.md).

## Reporting bugs

Open a [new issue](../../issues/new/choose) and pick the **Bug report**
template.

For "how do I..." questions, please use
[Discussions](../../discussions) instead.

## Contributing code

Bug fix PRs are welcome. For any change to what icons this patch
bundles, please open an issue first to discuss the design as the
patch's scope is deliberately narrow (assets from Proper 4K UI Project
under CleanSlate's names / ordering).

The technical reference (repo layout, DDS handling, PIL / GIMP
workflow, commit conventions) lives in [AGENTS.md](AGENTS.md). The
notes below cover only the in-game verification an automated agent
can't do for you.

### Testing your changes in-game

There's no automated test suite — verification is visual, in-game.
The fastest loop:

1. Copy or junction the mod into your CK2 mod directory
   (`Documents/Paradox Interactive/Crusader Kings II/mod/`).
2. Launch CK2 with the patch enabled alongside CleanSlate and Proper 4K
   UI Project.
3. Check `logs/setup.log` for lines mentioning
   `Proper4KUICleanSlatePatch` — confirms the mod loaded.
4. Load any save and inspect trait / modifier icons for the assets you
   changed. Compare against the same icon without the patch enabled.

For trait icons: `add_trait <trait_id> <charID>` in console, then
inspect the character sheet.

For modifier icons: `add_modifier <modifier_id> <charID> -1` in
console, then inspect the character sheet.

### Pull request workflow

1. Fork the repo.
2. Create a branch from `main` for your change.
3. Make and test your changes (see Testing above).
4. Commit with the [convention from AGENTS.md](AGENTS.md#conventions)
   (release-prefixed subject `vX.Y.Z - <topic>`, optional bullet body,
   CHANGELOG entry in the same commit).
5. Open a PR against `main` with a brief description of what changed
   and why.

## License

By contributing, you agree that your contributions are licensed under
the same **MIT License** that covers this patch's packaging. Icons
bundled from Proper 4K UI Project carry their author's licensing.
