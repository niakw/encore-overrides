# Encore Overrides

PS5-specific global and per-game profiles for **Prospero.Eden Encore**.

This repository is a **hardware-derived configuration database**. It provides:

- general Encore profiles used when no game-specific override exists;
- game-specific profiles;
- technical evidence explaining why each baseline exists.

## Profile tiers

Encore Overrides uses one clear quality ladder everywhere:

1. **Minimum**
2. **Recommandé**
3. **Haute**
4. **Ultra**

Internal IDs remain language-neutral:

`minimum` · `recommended` · `high` · `ultra`

## Resolution order

```text
Encore general profile
        ↓
game-specific encore-overrides profile
        ↓
user manual per-game settings
```

The most specific layer wins.

## General profiles

### Minimum

Lowest-load general baseline.

- Vulkan
- Docked
- **1x**
- **1080p**
- Bilinear
- AA None
- 60 Hz

### Recommandé

Default balance.

- Vulkan
- Docked
- **1.25x**
- **1440p**
- Bilinear
- **FXAA**
- 60 Hz

A 1080p-class Switch source at 1.25x is approximately **2400×1350**, close to native 1440p output.

### Haute

Higher image quality while preserving meaningful headroom below full 4K internal rendering.

- Vulkan
- Docked
- **1.5x**
- **2160p**
- **Bicubic**
- **FXAA**
- 60 Hz

For a 1080p-class source, 1.5x is approximately **2880×1620**. This costs 2.25× the pixels of 1x, versus 4× at 2x.

### Ultra

Maximum useful general image-quality ceiling.

- Vulkan
- Docked
- **2x**
- **2160p**
- Bilinear
- AA None
- 60 Hz

For a 1080p-class Switch render, 2x produces exactly **3840×2160**. This is the useful general ceiling for a 4K display. 3x and 4x remain available in Encore but are supersampling tiers, not sensible general defaults.

## Pixel workload

| Scale | Pixel workload vs 1x |
| --- | ---: |
| 0.75x | 0.5625× |
| 1x | 1.00× |
| 1.25x | 1.5625× |
| 1.5x | 2.25× |
| 2x | 4.00× |
| 3x | 9.00× |
| 4x | 16.00× |

## Game-specific overrides

Game-specific files reuse the same four profile IDs, but their actual values may differ according to the game's technical characteristics.

Current entry:

- **EA SPORTS FC 27** — `0100C49025D3E000`

Its profiles are:

| Tier | Game resolution | TV output | Filter | AA |
| --- | ---: | ---: | --- | --- |
| Minimum | 0.75x | 1080p | AMD FSR | None |
| Recommandé | 1.25x | 1440p | Bilinear | FXAA |
| Haute | 1.5x | 1440p | Bilinear | FXAA |
| Ultra | 2x | 2160p | Bilinear | None |

FC27 remains a 30 FPS-targeted Switch title, so every profile uses 60 Hz output for clean 2:1 presentation cadence.

## Files

```text
general/
  minimum.json
  recommended.json
  high.json
  ultra.json

games/
  <TITLE_ID>.json

manifest.json
SOURCES.md
```

No keys, firmware, games, dumps, copyrighted game assets or save data are stored here.
