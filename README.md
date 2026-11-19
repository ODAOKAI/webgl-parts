# PARTS·VIEWER

*A museum-grade showcase of mechanical engineering, sculpted entirely in mathematics and light.*

**PARTS·VIEWER** is a real-time 3D exhibition of precision mechanical components, rendered in raw **WebGL2** — no frameworks, no libraries, no assets. Every vertex you see was born from an equation: gears extruded from parametric tooth profiles, threads swept as triangular ridges along helical curves, impeller blades twisted station by station through curved airfoil space. It is a single HTML file that behaves like a professional CAD viewer wrapped in the atmosphere of a dark, cinematic gallery.

---

## The Collection

Five procedurally-generated artifacts rest upon a glass-like exhibition floor:

| № | Component | Craftsmanship |
|---|-----------|---------------|
| 01 | **Spur Gear** | Parametric tooth contour extrusion with machined chamfers, a five-spoke lightweight web, and a shouldered hub with a genuine bore. |
| 02 | **Hex Bolt** | A triangular thread profile swept along a true helix — real geometry, not a normal map — crowned by a chamfered hex head and washer face. |
| 03 | **Impeller** | Nine backward-curved blades, each a twisted doubly-curved thin plate with rim banding, mounted on a tapered hub over a dished base plate. |
| 04 | **Flange Coupling** | A true *assembly* — shaft, twin flanges, and eight instanced bolt-and-nut sets — that disassembles in mid-air when you pull the explode slider. |
| 05 | **Coil Spring** | A helical centerline whose pitch is integrated coil-by-coil, closing tight at both ends like a real compression spring's squared ends. |

## The Craft Beneath the Pixels

- **Pure WebGL2 pipeline** — instanced draw calls, uniform-driven materials, `VAO` geometry caches; not a single dependency.
- **Cinematic metal shading** — a procedural studio environment (warm key strip, cool rim strip, overhead softbox) feeds Fresnel-weighted reflections, so steel actually looks *machined*.
- **A living floor** — true planar mirror reflections beneath a fading dual-scale engineering grid, ringed by slowly orbiting holographic guide circles.
- **Honest shadows** — geometry projected onto the floor plane and de-duplicated through the stencil buffer, yielding one clean silhouette.
- **A full post-processing chain** — MSAA ×4 multisampled HDR rendering, quarter-resolution Gaussian bloom, ACES filmic tonemapping, vignette, and a whisper of film grain.
- **Atmosphere** — drifting dust motes, an orientation gizmo tucked into the corner viewport, and buttery damped camera motion on every control.

## Running It

There is nothing to install and nothing to build.

```bash
# either open the file directly
open index.html

# or serve it
python3 -m http.server 8765
# → http://localhost:8765
```

Any modern browser with WebGL2 support (Chrome, Edge, Firefox, Safari 15+) will do.

## Controls

| Gesture | Action |
|---------|--------|
| Drag | Orbit the part |
| Scroll | Zoom |
| Right-drag / Shift-drag | Pan |
| `1` – `5` | Switch components |
| `W` | Wireframe overlay |
| Double-click | Reset the camera |
| Explode slider | Disassemble the coupling |
| Reflection slider | Tune the studio environment intensity |

## Inside the Machine

The entire viewer lives in one file. A tiny linear-algebra kit feeds a small family of parametric surface builders — `lathe`, `extruded annulus`, `helical sweep`, `grid surface` — whose outputs merge into indexed meshes. Each mesh ships to the GPU as an instanced VAO, sharing a single shader that handles mirrored reflection, flattened shadows, emissive linework, and point sprites through uniform modes. The frame is a short choreography: mirror pass → floor → stenciled shadow → beauty pass → glow accents → corner gizmo → MSAA resolve → bloom → final grade.

*Built to prove that a thousand lines of careful mathematics can feel like magic.*
