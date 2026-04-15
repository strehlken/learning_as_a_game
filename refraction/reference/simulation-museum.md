# Simulation Museum

Reference collection of the best existing refraction and wave simulations. What each does, why it matters, how it relates to what we're building. HTML source files should be saved alongside this document for anything we want to study or reproduce.

---

## 1. Walter Fendt — Huygens Construction

**URL:** https://www.walter-fendt.de/html5/phen/refractionhuygens_en.htm
**Save as:** `fendt-huygens.html`

Step-by-step walkthrough of the Huygens construction. Pure HTML5 canvas, no dependencies. Originally a Java applet from 1998, ported to HTML5. Three input fields (n₁, n₂, angle), three buttons (Next step, Pause/Resume, Reset), one canvas, one text box narrating each step.

You press "Next step" repeatedly. A wavefront approaches the boundary. It hits at the incidence angle. Secondary circular wavelets expand from each contact point at different speeds per medium. The common tangent is drawn — that's the new wavefront. The refracted ray is perpendicular to it. Yellow = fast medium, blue = slow.

**Why it matters:** The purest pedagogical kernel of Huygens applied to refraction. Discrete steps force you to see each part of the construction. The tangent line is the entire punchline.

**What it lacks:** No continuous animation. No dispersion. No beam envelope. No comparison to wrong models.

**Relationship to our engine:** Our engine does the same construction continuously, with the tangent computed geometrically. Fendt likely uses Snell to place the tangent — need source to confirm.

---

## 2. Falstad Ripple Tank

**URL:** https://www.falstad.com/ripple/Ripple.html
**Source:** https://github.com/pfalstad/ripplegl
**Save as:** clone the repo

Full 2D wave equation solver. WebGL. Select "Example: Refraction." The domain is split into two regions with different propagation speeds. Solves ∂²u/∂t² = v²∇²u on a grid. A plane wave source generates wavefronts that refract at the boundary. Bending emerges from the differential equation — no Snell, no Huygens, no geometry. The Laplacian ∇² is literally the coupling: each point depends on its neighbors. Soldiers have no Laplacian.

**Why it matters:** Ground truth. Huygens behavior emerges from the wave equation rather than being drawn. Verification target for our engine.

**What it lacks:** Not pedagogical — you see the result, not the mechanism. Hard to read quantitatively.

---

## 3. PhET Bending Light

**URL:** https://phet.colorado.edu/en/simulations/bending-light
**Source:** https://github.com/phetsims/bending-light (MIT license)
**Save as:** clone the repo (complex multi-file app)

Gold standard pedagogical sim. Three tabs: Intro (single boundary), Prisms (shapes), More Tools (wave view, intensity). Ray-tracing core — computes Snell angle and draws rays. Wave toggle shows a sine wave that compresses in glass. Color slider changes refracted angle through dispersion. Prism tab produces rainbows.

**Why it matters:** UX benchmark. Clean, intuitive, widely trusted, used in university labs worldwide. The wave view is what our sine-wave-through-glass was trying to be.

**What it lacks:** The beam bends because the code applies Snell, not because wavelets propagate. No mechanism visible — result without why. Huygens never shown.

**Relationship to our engine:** PhET's polish + our physics = the dream.

---

## 4. Our Rigid Pole Problem

**File:** already in refraction/the-rigid-pole-problem.html

Huygens wavelets and marching soldiers side by side, showing they produce different refraction angles. The only simulation we can find that proves the soldier model gives the wrong angle. Three-tier taxonomy (no coupling → rigid rod → Huygens) is an original finding.

Built to convince, not to explore. The wavelet code here is the ancestor of the current engine.

---

## 5. Our Sine Wave Through Glass

**File:** already in refraction/sine-wave-through-glass.html

Negative example. Every point moves in the beam direction at local speed. Crests tilt but the beam envelope doesn't change direction. Demonstrates that "crests tilt" ≠ "beam bends." This is marching soldiers as a continuous wave.

---

## The Landscape

| Sim | What drives refraction | Shows mechanism | Beam bends | Dispersion |
|---|---|---|---|---|
| Fendt | Huygens (step-by-step) | Yes — circles + tangent | Implicit | No |
| Falstad | Wave equation (∇²) | No — emergent result | Yes | Configurable |
| PhET | Snell's formula | No — visualization only | Yes | Yes |
| Our rigid pole | Huygens vs soldiers | Yes — both models | No (not the point) | No |
| Our sine wave | Nothing (all go straight) | Shows the failure | No | No |
| **Our engine** | **Huygens geometric tangent** | **Yes** | **Yes** | **Next layer** |

---

## Collecting source files

Use Claude Chrome (View Source) or browser Save As:
1. **Fendt:** likely a single self-contained HTML. Most useful to study.
2. **Falstad:** clone `pfalstad/ripplegl` from GitHub. Multi-file WebGL app.
3. **PhET:** clone `phetsims/bending-light` from GitHub. Complex multi-file.

Fendt is the one most likely to fit in a single file and yield useful implementation details.
