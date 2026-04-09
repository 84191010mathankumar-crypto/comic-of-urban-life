# Isometric City — Parallel Layers

## Project overview

An interactive isometric city visualisation that renders physical urban space (benches, streets, plazas, façades) and abstract data layers (WiFi density, Bluetooth music streams, pedestrian flow, dwell time, memory traces) simultaneously and in parallel — exploring the concept that people experience the same city as multiple overlapping realities.

The entire project is a single self-contained HTML file with no external dependencies.

---

## File structure

```
isometric_city/
├── index.html   ← the entire application (HTML + CSS + JS, no dependencies)
└── CLAUDE.md    ← this file
```

---

## How to open

**Browser (simplest):**
```bash
open index.html
# or on Linux:
xdg-open index.html
```

**Local dev server (avoids any CORS quirks):**
```bash
npx serve .
# then visit http://localhost:3000
```

**VS Code Live Server:**
Right-click `index.html` → Open with Live Server.

---

## Architecture

Everything lives in `index.html`. The structure inside is:

| Section | What it does |
|---|---|
| `<style>` | Dark-theme CSS for the UI panel, toggles, stat cards, tooltip |
| `#scene` + `<canvas>` | The isometric 3D city rendered via Canvas 2D API |
| `#ui` | Time-of-day slider, layer toggles, live stat cards |
| `<script>` | All simulation logic and rendering |

### Key functions

| Function | Purpose |
|---|---|
| `iso(gx, gy, gz)` | Isometric projection: grid coords → screen pixels |
| `box(...)` | Draw a single isometric box (top face + two side faces) |
| `drawBench/Plaza/Street/Facade(p)` | Render each place type using composed `box()` calls |
| `drawGround()` | Checkerboard isometric ground plane |
| `drawWifi()` | Expanding elliptical rings per WiFi node, scaled by probe count |
| `drawFlow(t)` | Animated particles travelling between connected places |
| `drawDwell()` | Vertical green bars above benches/plazas showing dwell minutes |
| `drawMem(t)` | Slow purple ripples encoding memory/archive density |
| `drawPerson(p)` | Stick figure with bobbing animation; gold BT pulse if streaming |
| `drawBtLabels(t)` | Floating artist names above Bluetooth-active people |
| `ts(h)` | Time-of-day activity curve — returns 0.05 (night) → 1.0 (noon) |
| `rebuild()` | Regenerates simulation data, people, WiFi rings for current hour |

---

## City places

| ID | Label | Type | Grid pos |
|---|---|---|---|
| `bA` | Bench A | bench | 1.5, 2.5 |
| `bB` | Bench B | bench | 5.5, 1.2 |
| `bC` | Bench C | bench | 0.5, 6.5 |
| `pM` | Main Plaza | plaza | 4.0, 5.0 |
| `pE` | East Plaza | plaza | 7.5, 3.5 |
| `sN` | North St | street | 3.0, 2.0 |
| `sE` | East St | street | 6.5, 5.0 |
| `fA` | Façade A | facade | 2.0, 6.0 |
| `fB` | Façade B | facade | 5.0, 2.0 |
| `fC` | Façade C | facade | 8.5, 5.5 |

Each place has base data values (`bD` dwell, `bW` WiFi, `bB` Bluetooth, `bF` flow) that are multiplied by the current `ts(hour)` curve and a small noise factor each time `rebuild()` runs.

---

## Data layers (toggle buttons)

| Toggle | What it shows |
|---|---|
| Physical | 3D isometric city objects |
| People | Animated stick figures distributed across places |
| WiFi rings | Expanding elliptical rings; ring size ∝ probe count |
| Bluetooth | Gold pulse rings on people + floating artist names |
| Flow paths | Orange dashed lines + travelling particles between places |
| Dwell bars | Green vertical bars above benches and plazas |
| Memory | Purple ripples encoding cumulative presence |

---

## Extending this project

### Add a new place
Add an entry to the `PLACES` array in `index.html`:
```js
{ id:'bD', label:'Bench D', type:'bench', gx:9.0, gy:7.0,
  bD:150, bW:3, bB:1, bF:10, c:'#2db87a' }
```
Types available: `'bench'`, `'plaza'`, `'street'`, `'facade'`.

### Add a new connection (flow path)
Add a pair to the `CONNS` array:
```js
['bD', 'pM']   // Bench D → Main Plaza
```

### Add a new place type
1. Write a `drawMyType(p)` function using `box()` calls.
2. Add a branch in the render loop: `else if (p.type === 'mytype') drawMyType(p);`

### Adjust time curve
Edit the `ts(h)` function. It returns a float 0–1 representing activity level for hour `h`.

### Add real data
Replace the `rebuild()` function's random noise with actual sensor readings. The `sim` object just needs `{ dwell, wifi, bt, flow }` per place ID.

---

## Design language

- **Physical layer:** warm earth tones — wood benches (`#c09060`), stone plazas (`#b8b09a`), asphalt streets (`#32323a`), concrete façades (`#c0b8a8`)
- **Bench / green:** `#2db87a` — rest and stillness
- **Plaza / amber:** `#e8a020` — gathering and warmth
- **Street / purple:** `#7b6ef0` — movement and flow
- **Façade / pink:** `#e8607a` — interface between private and public
- **WiFi rings:** `rgba(80,180,255,…)` — blue, cool, informational
- **Flow particles:** `rgba(255,160,70,…)` — orange, warm, kinetic
- **Memory ripples:** `rgba(160,90,255,…)` — purple, slow, archival
- **BT pulses:** `rgba(255,210,70,…)` — gold, personal, musical
