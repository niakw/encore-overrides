# Encore Overrides

PS5-specific game profiles for **Prospero.Eden Encore**.

## Method

Every profile is derived in this order:

1. **Source console hardware** — for current games, Nintendo Switch 1.
2. **The game's documented target on that console** — frame rate, rendering resolution/mode when reliably measured, engine behaviour.
3. **Encore/Eden emulation overhead** on a standard PS5.
4. **PS5 headroom** used to improve image quality only while preserving gameplay and stability.
5. **Real-hardware validation** before automatic application.

Personal observations are **not** used to author the initial candidate. They are only used afterward to validate or reject it.

## Status

For now this repository deliberately contains **one candidate game only**:

- EA SPORTS FC 27 — `0100C49025D3E000`

We will validate this methodology before expanding to other Switch games.

## FC 27 candidate

| Setting | Recommended candidate |
| --- | --- |
| Renderer | Vulkan |
| Console mode | Docked |
| Game resolution | **1.25x** |
| TV output | **1440p** |
| Upscaling | **Bilinear** |
| Anti-aliasing | **None** |
| Refresh | **60 Hz** |
| Target | **stable 30 FPS** |

### Why 1.25x / 1440p?

The Frostbite-era Switch version of FC 24 is documented at 1080p docked / 30 FPS, while FC 25 remains a 30 FPS title on Switch. FC 27's exact Switch 1 internal resolution has not yet been independently established, so it is not invented here.

Using the documented 1080p Frostbite baseline as an engineering reference:

- 1.00x ≈ 1920×1080
- **1.25x ≈ 2400×1350**
- 1.50x ≈ 2880×1620

2400×1350 is already very close to a 2560×1440 output, so 1.25x + Bilinear requires little reconstruction. Moving to 1.50x computes about **44% more pixels** than 1.25x, for a smaller visual gain and less emulation headroom.

No extra FXAA/SMAA is enabled by default because the candidate should not add another post-process AA pass without game-specific evidence that it improves the image.

## Files

- `games/0100C49025D3E000.json` — machine-readable candidate.
- `SOURCES.md` — technical evidence used to derive it.
- `validation/0100C49025D3E000.md` — hardware test protocol.

## Rule

Candidate profiles use `auto_apply: false`.

Only after repeatable real-PS5 testing may a profile become `validated` and be considered for automatic application.

No keys, firmware, games, dumps, copyrighted game assets or save data are stored here.
