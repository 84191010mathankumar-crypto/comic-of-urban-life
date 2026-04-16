# Comic of Urban Life

**An interactive multi-layer city explorer that renders the invisible digital life of urban space in parallel with its physical reality.**

| | |
|---|---|
| **Author** | [Your name] |
| **Studio** | Prompt City — Urban Vision Wolfsburg 2026 |
| **Course** | IUDD Master, SoSe 2026 |
| **Chair** | Informatics in Architecture and Urbanism (InfAU), Faculty of Architecture and Urbanism, Bauhaus-Universität Weimar |
| **Teaching staff** | Reinhard König, Martin Bielik, Sven Schneider, Egor Gaydukov, Egor Gavrilov |
| **Exercise** | Urban Absurdities (Nonsense Project) |
| **Submission date** | 2026-04-16 |

---

## Links

- **Live app (GitHub Pages):** https://84191010mathankumar-crypto.github.io/comic-of-urban-life/
- **Source repo:** https://github.com/84191010mathankumar-crypto/comic-of-urban-life
- **Miro frame:** https://miro.com/app/board/uXjVGCtKivA=/?moveToWidget=[your-frame-id]
- **60 s showreel:** embedded on the Miro frame above

---

## The task

Nonsense Project is a two-weeks long task designed to get familiar with application of coding agents in building apps, tools and projects that investigate unique ways of working with urban context. I was randomly assigned one urban paradox and one constraint from the studio's Nonsense Ideas deck and built a working web app that answers this combination. The process is documented here and in a 60-second showreel.

---

## Theme & constraint

**Theme (Urban Absurdity):**
[Paste the theme exactly as drawn.]

**Constraint (Playful Limitation):**
[Paste the constraint exactly as drawn.]

---

## Concept and User Story

### Concept

Comic of Urban Life treats the city as a stack of simultaneous, overlapping realities rather than a single physical place. The same bench, plaza, or street corner is experienced entirely differently depending on whether you read the wood-and-stone layer or the invisible digital layer humming above it — WiFi probe counts, Bluetooth music streams, pedestrian dwell time, memory traces. The app renders both layers at once, in an isometric comic-book view, making the absurd density of concurrent urban experience legible in a single glance. The constraint bites in the simulation itself: every data value is regenerated on a fixed time curve, so the city's "mood" shifts hour by hour, and the user cannot freeze or rewind it — only observe the present moment.

### User Story

Elena is a 34-year-old urban-data researcher visiting Wolfsburg for a conference. She finds the link in a fellow attendee's slide deck and opens it on her phone during a coffee break, curious whether it is another dull dashboard. The isometric city loads — warm earth tones, benches, plazas, a few stick figures bobbing — and she drags the time slider to 02:00 just to see what the city looks like at night. The WiFi rings shrink almost to nothing; the dwell bars above the benches flatten. She switches on Bluetooth and watches gold pulse rings appear around two lonely figures still streaming music in the dark plaza. She cycles back to 12:00 and the city explodes with orange flow-particles threading between every node. She toggles Physical off, leaving only the data layers floating in space, and realises she is looking at a city that exists entirely without buildings. She feels a mild unease — the data-city is busier and more legible than the stone-and-wood one. She takes a screenshot and sends it to her group chat with the caption: *"the city that runs on top of the city."*

---

## How to use it

1. **Open the live app** — you land on the intro screen (`intro.html`). Click **Enter** to reach the main isometric view.
2. **Drag the time slider** (top-left) from 00 to 23 to watch the city's activity pulse through a full day.
3. **Toggle layers** using the buttons in the sidebar: Physical · People · WiFi rings · Bluetooth · Flow paths · Dwell bars · Memory.
4. **Hover any place** (bench, plaza, street, façade) to see a tooltip with live data for that node.
5. **Try this for the most interesting behaviour:** turn Physical *off*, then enable all data layers — you see the invisible city floating without architecture.
6. **Globe view** (`globe.html`) — navigate back to the intro and choose Globe to see the data-city projected onto a spinning globe canvas.

---

## Technical implementation

| | |
|---|---|
| **Frontend** | Vanilla JS + Canvas 2D API, single self-contained HTML file per view (no build step) |
| **Hosting & build** | GitHub Pages, deployed from `main` branch (no CI workflow) |
| **Data sources / APIs** | None — all simulation data is generated procedurally in-browser |
| **Models at runtime** | None |
| **Notable libraries** | Google Fonts (Outfit, Inter, DM Mono) via CDN — display only |

### Run locally

```bash
# Option 1 — static server (recommended)
npx serve .
# then open http://localhost:3000

# Option 2 — VS Code
# Right-click index.html → Open with Live Server

# Option 3 — just open the file
open index.html
```

---

## Working with AI

**Coding agents used:** Claude Code · model `claude-sonnet-4-6`

**Key prompts that moved the project:**

> "Build a single self-contained HTML file that renders an isometric city with toggleable data layers — WiFi rings, Bluetooth pulses, pedestrian flow particles, dwell bars, and memory ripples — all animated on a Canvas 2D context with no external dependencies."

> "Add a time-of-day slider that rebuilds the simulation data and smoothly transitions all layer intensities through a day/night activity curve."

> "Create an intro landing page (comic-book aesthetic, halftone texture, cream background) that links to the main city view and to a globe view."

> "Build a globe.html — a dark, spinning 3D globe rendered on Canvas 2D using an orthographic projection, with city nodes plotted as glowing points and animated arc connections between them."

**Reflection:** The agent was fastest when given a precise visual and behavioural target in a single prompt — monolithic "build X with these exact properties" requests produced working code immediately, whereas incremental "now add Y" follow-ups sometimes required two or three correction rounds because the agent lost track of existing variable names. The one thing I would do differently: write a short spec document first and paste it into the opening prompt, so the agent holds the full system model from the start rather than accumulating it turn by turn.

---

## Credits, assets, licenses

| | | |
|---|---|---|
| **Fonts** | Outfit, Inter, DM Mono | Google Fonts, SIL Open Font License |
| **Data** | None — all data is procedurally simulated | — |
| **Images / sounds** | None | — |
| **Third-party code** | None | — |

**This repo:** MIT
