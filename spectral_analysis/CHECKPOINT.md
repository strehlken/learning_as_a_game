# Spectral Analysis — Session Checkpoint (2026-04-11)

## What exists

- **index.html** — Main app with four sections:
  1. Experiment animation (prism + apparatus) with periodic table for element selection
  2. Compare causes (Earth vs Sirius vs Betelgeuse)
  3. Read a real star (overlay explored elements)
  - Multi-element selection (click to toggle)
  - Quick gases as shortcuts
  - Emission / absorption toggle
  - Discrete rays / continuous beam toggle (absorption mode)
  - Full NIST spectral data for all 118 elements (inline)
  - Sellmeier dispersion for refraction angles, but wave rendering is NOT physically exact

- **index_experiment.html** — Work-in-progress experiment file attempting exact physics
  - Has Sellmeier/Snell ray tracing (SF11 glass, 55° apex, 48° incidence, -0.62 rad rotation)
  - Lagrangian wave drawing attempted but joints/boundaries not correct yet
  - Layout: prism left, source compressed, detector on right edge

- **reference.html** — Codex's physically exact prism (original Eulerian approach, good Sellmeier/Snell, but fixed step-count wave drawing)

- **reference_2.html** — The correct approach (from Codex). Particle simulation:
  - Each particle carries a fixed sine value from birth
  - Moves at c in air, c/n in glass
  - State transitions by testing `inTri()` against the actual drawn prism triangle
  - Wave shape emerges from particles bunching up — not computed
  - Sharp direction changes at boundaries happen naturally
  - This is the model to follow

- **DIALOGUE.md** — Full Claude-Codex dialogue on pedagogy and design
- **spectral-data.js** — Extracted NIST data (not referenced by current index.html, which has data inline)

## What needs to happen next

1. **Adopt the particle simulation from reference_2.html into index_experiment.html**
   - Use the `Channel` class / particle approach from reference_2
   - Keep our layout: prism toward left, source/gas/slit compressed, detector vertical on right
   - Keep our Sellmeier data, element data, emission/absorption modes
   - Test state transitions against the drawn prism triangle (`inTri`), not precomputed segments
   - Larger amplitude than reference_2 (Nick wants wide visible waves)
   - Choose parameters (incidence, apex, glass, rotation) so the fan fits our layout horizontally

2. **Once index_experiment.html works correctly, integrate it back into index.html**
   - Replace the current hand-waved experiment animation
   - Keep everything else (periodic table, compare causes, star reading, multi-element selection)

3. **Polish items from earlier that still apply:**
   - Periodic table is cramped at 18 columns — consider better layout
   - Lab-to-star connection could feel more direct
   - The continuous beam mode in absorption should show dark waves at absorbed wavelengths prominently

## Key physics principles to preserve

- All wavelengths travel at the same speed c in air
- In glass, speed = c/n(λ) where n comes from Sellmeier equation
- Wavelength contraction inside glass emerges from particles bunching up (not computed separately)
- Frequency is invariant across all media
- State transitions happen at the actual drawn prism boundary
- Snell's law determines the direction change at each face
- Phase/sine value is carried by each particle from birth — never recomputed

## Design principles

- Font: Brandon Grotesque, system-ui, sans-serif
- Background: #f7f8fa, text: #232324
- Canvas background: #e8ecf2 (slightly darker so white beams show)
- Self-contained HTML (no external local dependencies)
- Deploys to GitHub Pages via git@github-strehlken
