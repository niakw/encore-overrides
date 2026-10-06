# Encore Overrides

PS5-specific game profiles for **Prospero.Eden Encore**.

Encore Overrides complements, rather than replaces, Eden's own compatibility overrides:

- **Eden overrides** fix emulator/game compatibility issues that can apply across multiple platforms.
- **Encore overrides** tune games for Encore's fixed PS5 environment and expose practical per-game profiles.

## Goals

- Recommended settings by Switch Title ID.
- PS5-specific `Recommended`, `Performance`, and `Quality` profiles.
- Explicit validation state so experimental data is never presented as proven.
- Known-problem combinations and game-specific notes.
- Versioned, machine-readable data that Encore can cache locally and refresh without requiring a full app release.
- Offline fallback: Encore can ship a known-good snapshot of this database.

## Repository layout

```text
games/
  <TITLE_ID>.json
schema/
  encore-override.schema.json
tools/
  validate.py
manifest.json
.github/workflows/validate.yml
```

## Profile precedence

Encore should resolve settings in this order:

```text
Encore factory/global settings
        ↓
Eden compatibility override
        ↓
Encore game profile
        ↓
User per-game override
```

A user override always wins. Selecting or editing values outside an authored Encore profile should surface as **Custom** in the UI.

## Validation states

- `experimental` — useful starting point, not yet fully hardware-qualified.
- `testing` — actively being measured/retested on PS5.
- `validated` — profile has passed the repository's validation requirements on the declared firmware/Encore build.
- `deprecated` — retained for history but should not be selected automatically.

Profiles also carry an individual confidence level: `provisional`, `tested`, or `validated`.

## Supported settings (schema v1)

The first schema intentionally mirrors the settings Encore currently exposes per game:

- renderer: Vulkan / OpenGL
- TV output: 1080p / 1440p / 2160p
- game resolution: 0.25x through 4x
- upscaling filter: Bilinear / AMD FSR / Bicubic / Nearest
- FSR sharpness: 0–100
- anti-aliasing: None / FXAA / SMAA
- refresh rate: 60 / 120 Hz
- console mode: Docked / Handheld

Low-level Eden internals are deliberately excluded until Encore exposes and validates a safe PS5 use case for them.

## First game

The initial entry is **EA SPORTS FC 27** (`0100C49025D3E000`). It is deliberately marked **experimental** while PS5 stability and image-quality work continues.

## Consuming the database

Encore should fetch `manifest.json`, verify `schema_version`, then load the matching file from `games/`.

The application should keep the last valid local copy and fail closed to bundled/default settings if downloaded data is malformed or targets an unsupported schema.

## Relationship with Eden

This repository is not affiliated with or endorsed by the Eden project. It is a PS5-specific companion database for Prospero.Eden Encore.

No keys, firmware, games, copyrighted console data, or game assets are stored here.
