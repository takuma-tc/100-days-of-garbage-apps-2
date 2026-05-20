# 100-days-of-garbage-apps-2

## Day 2 — Sand Lab

A falling sand simulation built as a single self-contained HTML file. No dependencies, no build step — just open `index.html`.

## Materials

| Key | Material   | Behavior |
|-----|------------|----------|
| `1` | Sand       | Falls, slides diagonally, floats on water |
| `2` | Water      | Falls, flows sideways up to 3 cells, freezes near ice, evaporates near fire |
| `3` | Wall       | Static solid |
| `4` | Fire       | Rises, spreads to oil/plant/gunpowder, melts ice, lifetime 60–120 ticks |
| `5` | Smoke      | Rises and disperses, fades out over 80–150 ticks |
| `6` | Oil        | Falls, floats on water, ignites on contact with fire |
| `7` | Lava       | Falls, ignites flammables, solidifies to wall when touching water or ice |
| `8` | Acid       | Falls like water, erodes sand/wall/ice/plant on contact |
| `9` | Steam      | Rises slowly, condenses back to water after ~200 ticks |
| `0` | Ice        | Static, freezes adjacent water, melts near fire or lava |
| `q` | Plant      | Static, grows slowly into empty cells, burns on contact with fire |
| `w` | Gunpowder  | Falls like sand, explodes in radius-4 chain reaction when ignited |

## Controls

| Input | Action |
|-------|--------|
| Left drag | Place selected material |
| Right drag | Erase |
| `1`–`9`, `0`, `q`, `w` | Select material |
| `C` | Clear canvas |
| `P` | Pause / Resume |

Brush size (1 / 3 / 5 cell radius) is selectable in the right panel.

## Technical notes

- Grid: 200×150 cells stored as a flat `Uint8Array`
- Renderer: `OffscreenCanvas` + `ImageData` written as `Uint32Array`, 3× pixel scale
- Update order: bottom-to-top, alternating left-right each frame to avoid directional bias
- A second `Uint8Array` dirty buffer skips already-processed cells per frame
- Explosion system applies a velocity impulse buffer (`Float32Array` × 2) to nearby particles
- Target 60 fps via `requestAnimationFrame`
