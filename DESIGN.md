# arnavrai.in design system (v8)

A tour of a physics lab: dark 3D stages for the big moments, lighter reading sections between them, a warp starfield behind everything, and an icon on nearly every item.

## Page order

Hero (collider) → marquee → Beacon → Research (digital twin) → Experience → Quark Talk → Work (constellation, 4 featured rows, 20-row index) → Space program (flight) → Research and leadership (bento) → Schoolhouse → Awards and skills → Fun facts → Contact.

## Scenes (three.js r128 from cdnjs; only on-screen scenes render)

| Section | Scene | Interaction |
|---|---|---|
| Hero | Collider event display | Click to fire, hold to stream collisions, the button fires a burst of 5; up to 12 events at once |
| Beacon | Real design, exploded by scroll, then a live demo | Hold 3 s or double-tap; green halo; ridged/smooth toggle |
| Research | Storage ring + digital twin | Scroll lifts the twin |
| Quark Talk | Proton + audio spectrum ring | Drag to rotate |
| Work | Constellation, one node per project, colored by category | Cycles a labelled highlight; filters dim nodes |
| Space | Pad → liftoff → x-ray of the DOLL-E payload inside the rocket → stage separation → fairing opens → PULSE-A CubeSat unfolds | Scroll drives the flight |
| Terminal | Rocket idling beside the console | `launch` or `party` sends it up |

## Color (no pink)

| Token | Light | Dark | Role |
|---|---|---|---|
| `--paper` / `--card` | `#EEF0F2` / `#F8F9FB` | `#0B1120` / `#111A2E` | Reading sections |
| `--ink` / `--graphite` | `#1B2440` / `#555D6E` | `#E4E8F0` / `#9BA4B6` | Text |
| `--accent` | `#2F5BE8` | `#7AA2FF` | Links, numbers, buttons on paper |
| `--stage` | `#060A16` | `#04070F` | 3D stages |
| `--blue` `--cyan` `--gold` `--green` `--teal` | `#5B8CFF` `#8FD3FF` `#FFC46B` `#47E58A` `#2BD9A8` | same | Category colors, tracks, beam, halo, terminal button |

Categories: ventures gold, simulations cyan, social impact green, tools and media blue.

## Icons

An inline SVG sprite at the top of `<body>` (`#i-rocket`, `#i-atom`, `#i-sat`, …). Use: `<svg class="ic"><use href="#i-rocket"/></svg>`.

## Editing notes

- Projects are the `<article class="card">` blocks in `#grid`: `data-cat` sets filter and constellation color, `data-art` picks the generative art, the `.badge` holds the icon.
- Beacon label text lives in the `.tag` elements, in the same order as the 3D layers.
- Terminal commands are in the `CMDS` object in the script.

## Motion and performance

- Desktop wheel scrolling glides at about 70% of native speed; any scrollbar drag or key scroll cancels the glide. Anchor links glide too. Reduced motion uses native scrolling.
- Pinned sections are longer (Beacon 560vh, Research 320vh, Space 520vh) so each step has room.
- The hero scene builds first; the rest build one at a time in idle time, or as soon as you scroll within about 1,400px of them. Pixel ratio is capped at 1.5.

## v6 additions

- Work: four featured projects as large rows with live generative art; the other twenty in an index with category and pricing pills and a live preview that follows the cursor. Pricing comes from Arnav's notes (free, paid, free and paid, government-subsidized).
- Research and leadership: a bento grid; each tile has its own live canvas (EEG traces, elliptic-curve point addition, GPS clocks, Bloch sphere, DNA helix, ridgelines, pixel arcade).
- Schoolhouse: gauge rings for hours, sessions, countries and learners; rating bars; certification progress; two rows of scrolling feedback that pause on hover. Numbers come from the October 30, 2026 portfolio.
- Space: textured UCSP airframe with an ogive fairing, launch rail, shader flame and smoke trail, procedural Earth (oceans, land, clouds, city lights, atmosphere), DOLL-E x-ray, a 3U CubeSat ejected from its dispenser with deploying wings and antennas, and a laser link.
- Ring: painted dipoles with copper coils, quadrupoles, sextupoles, an RF cavity, flanges, blinking beam position monitors, three bunches, synchrotron light at the bends, and a betatron orbit trace on the twin.
- Hero: jet cones, muons reaching the outer chambers, and ambient bunches along the beam pipe.
- Responsiveness: cursor follows at 0.42 per frame, wheel glide eases at 0.12, hover transitions are 0.12 to 0.18 s, reveals 0.6 to 0.85 s.

## v7 additions

- Page order: … Schoolhouse → Awards and skills → Sports (cricket scene) → Hobbies → Fun facts → Contact.
- Sports: the batsman is a neon outline drawn as glowing strokes between joints (head, torso, arms, legs, pads, bat), pivoting at the hips so nothing can dislocate. The ball has an emissive core, halo, comet trail, point light, a spark burst and a shockwave at impact; scene time runs at 30% through the hit (about a five-second loop).
- Terminal: typing happens inline at a `guest@arnavrai:~$` prompt with a blinking caret; clicking anywhere in the window focuses it. The rocket pane initialises after the window opens so the UI never waits on it.
- Cursor: dot and ring are positioned directly from the pointer, with no smoothing.
- UCSP logo: embedded inline (base64) above the Space program heading, so it needs no extra file.
