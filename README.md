# Encore Overrides

PS5-specific per-game profiles for **Prospero.Eden Encore**.

This repository is a **hardware-derived baseline database**, not a test registry. Profiles are authored from the source console, the game's known technical target, Encore's own PS5 presets and the fixed characteristics of a standard PS5.

## Method

Profiles are derived in this order:

1. **Source console hardware** — Nintendo Switch 1 for the current database.
2. **Game target on source hardware** — frame rate, docked/handheld mode and measured rendering characteristics when trustworthy data exists.
3. **Standard PS5 hardware** — fixed CPU/GPU/memory target.
4. **Encore/Eden emulation overhead** — preserve headroom rather than treating PS5/Switch raw-spec ratios as a direct resolution multiplier.
5. **Encore's built-in presets** — use them as conservative PS5 reference points.
6. **Game-specific profile adjustment** — Recommended, Smooth and Performance.

Profiles are usable baselines and may be auto-applied. They do not require a validation gate.

## EA SPORTS FC 27

Title ID: `0100C49025D3E000`

The Switch Frostbite FC line targets **30 FPS**, with FC 24 documented at **1080p docked / 720p handheld** and FC 25 remaining at 30 FPS. FC 27's exact Switch 1 internal pixel count is not claimed when no reliable direct measurement exists.

### Recommended

Best balance of graphics, playability and stability.

| Setting | Value |
| --- | --- |
| Renderer | Vulkan |
| Console mode | Docked |
| Game resolution | **1.25x** |
| TV output | **1440p** |
| Upscaling | **Bilinear** |
| FSR sharpness | 50% — inactive with Bilinear |
| Anti-aliasing | **FXAA** |
| Refresh | **60 Hz** |
| Gameplay target | **30 FPS** |

This starts from Encore's built-in Recommended preset and changes only the internal scale from 1x to 1.25x.

### Smooth

Prioritizes consistent frame pacing while preserving a native-class internal render scale.

| Setting | Value |
| --- | --- |
| Renderer | Vulkan |
| Console mode | Docked |
| Game resolution | **1x** |
| TV output | **1080p** |
| Upscaling | **Bilinear** |
| FSR sharpness | 50% — inactive with Bilinear |
| Anti-aliasing | **None** |
| Refresh | **60 Hz** |
| Gameplay target | **30 FPS** |

### Performance

Maximizes GPU headroom while keeping a usable 1080p image.

| Setting | Value |
| --- | --- |
| Renderer | Vulkan |
| Console mode | Docked |
| Game resolution | **0.75x** |
| TV output | **1080p** |
| Upscaling | **AMD FSR** |
| FSR sharpness | **40%** |
| Anti-aliasing | **None** |
| Refresh | **60 Hz** |
| Gameplay target | **30 FPS** |

## Profile behavior

- `Recommended` is the default profile.
- `Smooth` reduces presentation/internal load without dropping below 1x.
- `Performance` deliberately drops to 0.75x and enables FSR reconstruction.
- A user's manual per-game settings should always override this database.
- No profile attempts to force a 60 FPS game simulation when the Switch title itself targets 30 FPS.

## Files

- `manifest.json` — database index.
- `games/<TITLE_ID>.json` — game-specific profiles.
- `SOURCES.md` — technical evidence used to derive profiles.

No keys, firmware, games, dumps, copyrighted game assets or save data are stored here.
