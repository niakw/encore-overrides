# Encore Overrides

PS5-specific global and per-game profiles for **Prospero.Eden Encore**.

This repository is a **hardware-derived configuration database**. It provides:

- general Encore profiles used when no game-specific override exists;
- game-specific Recommended / Smooth / Performance profiles;
- technical evidence explaining why each baseline exists.

## Resolution order

Encore should resolve profiles in this order:

```text
Encore general profile
        ↓
game-specific encore-overrides profile
        ↓
user manual per-game settings
```

The most specific layer wins.

## General profiles

The general files live in:

```text
general/
  recommended.json
  smooth.json
  performance.json
```

They are derived from Nintendo Switch 1 hardware, a standard/original PS5 and the settings actually exposed by Encore/Eden.

### Recommended — best-case / maximum useful quality

| Setting | Value |
| --- | --- |
| Renderer | Vulkan |
| Console mode | Docked |
| Game resolution | **2x** |
| TV output | **2160p** |
| Upscaling | Bilinear |
| Anti-aliasing | None |
| Refresh | 60 Hz |

For a 1080p-class docked Switch render, 2x produces **3840×2160**, exactly matching 4K output. This is the useful general ceiling: 3x and 4x render beyond a 4K display and mainly spend GPU/memory on supersampling.

### Smooth — high quality with large headroom

| Setting | Value |
| --- | --- |
| Renderer | Vulkan |
| Console mode | Docked |
| Game resolution | **1.25x** |
| TV output | **1440p** |
| Upscaling | Bilinear |
| Anti-aliasing | FXAA |
| Refresh | 60 Hz |

For a 1080p-class source, 1.25x is approximately **2400×1350**, already close to 1440p while using only **39.1% of the internal pixel workload of 2x**.

### Performance — native-class fallback

| Setting | Value |
| --- | --- |
| Renderer | Vulkan |
| Console mode | Docked |
| Game resolution | **1x** |
| TV output | **1080p** |
| Upscaling | Bilinear |
| Anti-aliasing | None |
| Refresh | 60 Hz |

The general Performance profile deliberately stays at 1x rather than degrading every unknown game to 0.75x. A demanding game can override this with 0.75x + FSR when justified.

## Why no global 3x / 4x?

Encore exposes those scales, but they are not sensible general defaults.

Relative internal pixel workload:

| Scale | Pixel workload vs 1x |
| --- | ---: |
| 1x | 1.00× |
| 1.25x | 1.56× |
| 1.5x | 2.25× |
| 2x | 4.00× |
| 3x | 9.00× |
| 4x | 16.00× |

A 1080p-class title already reaches 4K at 2x. Going above that is supersampling and should be treated as a game-specific experiment, not a general PS5 profile.

## Game overrides

Game-specific profiles live under `games/<TITLE_ID>.json` and replace the matching general profile when present.

Current game-specific entry:

- **EA SPORTS FC 27** — `0100C49025D3E000`

FC27 uses its own lighter profiles because its Frostbite workload and 30 FPS target justify a different balance than the best-case global ceiling.

## Method

Profiles are derived from:

1. source-console hardware and output characteristics;
2. known game rendering target when a game override exists;
3. standard PS5 CPU/GPU/memory characteristics;
4. Encore/Eden's actual exposed renderer, scale, output, filter, AA and refresh settings;
5. preservation of emulator headroom rather than raw-spec multiplication.

No user-specific observations are required to author the general profiles.

## Files

- `manifest.json` — database index and general fallback mapping.
- `general/*.json` — global Encore profiles.
- `games/<TITLE_ID>.json` — game-specific profiles.
- `SOURCES.md` — technical evidence.

No keys, firmware, games, dumps, copyrighted game assets or save data are stored here.
