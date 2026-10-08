# Visual PlayStation glyphs (in-game artwork) — curated rules

Eden Encore now reads a separate catalogue alongside the existing video/performance profiles:

    glyphs/manifest.json

It is a compatibility list for **visible graphics drawn by each Switch game**,
not the DualSense controller mapping. No native Nintendo assets are shipped.

A verified title rule looks like:

    {"title_id":"0100123456789000",
     "update_version":"v1.2.0",
     "build_id":"0123456789ABCDEF0123456789ABCDEF01234567"}

The IDs above are illustrative only and **must not be added** as a real rule.
Only add a title after its exact update version and build identity are known
and a legally distributable PlayStation graphic replacement pack has been
tested. The catalogue currently contains **zero verified titles**.

Eden Encore syncs this manifest to data/glyph-overrides.json and generates
headless/glyph_overrides_generated.h with
tools/sync-glyph-overrides.py --source /path/to/encore-overrides.

On PS5, only a matching installed LayeredFS RomFS graphics pack named
Eden Encore PS Glyphs can become active. Missing packs, unknown version,
or unsupported title always retain the original Nintendo game prompts.
A separate global setting (/appearance/ingame_button_glyphs) and optional
per-title setting (/games/TITLE/ingame_button_glyphs) accept 'playstation'
(default) or 'switch'. Neither changes what DualSense buttons do.

**Important limit:** The current Eden metadata bridge can read the latest
update's display version, not attest the actual running program's build ID.
The installer independently checked the original dumped RomFS graphic hashes
when staging the pack, but native effective-build verification is still
required before this is a production-grade automatic visual feature.
Unverified title updates, gameplay glyph coverage, and firmware testing
remain tracked at https://github.com/niakw/Prospero.Eden-Encore/issues/7.
