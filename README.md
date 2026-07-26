# LATM: Hive Infiltration

Free playable episodes set in the world of **Life After The Machines**,
funneling players to Book 1.

- **Chapter 1 — The Hive**: Marcus wakes inside a machine hive, fights
  through three corridor segments, and plants a charge at the core.
- **Chapter 2 — The Processing Center** (`#ch2`): armed from the start,
  Marcus crosses the cylinder halls from the book — including cylinder
  A-113, ANGELA M. — and pulls the ledger of taken names while wardens
  (heavy sentry frames) defend the control room.

Chapters are pure data objects in `CHAPTERS` inside `index.html`
(rooms, drones, radio script, palette, props); the engine builds
whichever the URL hash selects. Adding a chapter = adding a data block.

## Play

Single file, no build step. Serve `index.html` from anywhere
(GitHub Pages works as-is). Three.js is loaded from the jsdelivr CDN.

- **Desktop:** WASD move, mouse look (click for pointer lock), click/Space fire, hold E to plant.
- **Mobile:** left side virtual stick to move, right side drag to look, FIRE button, hold PLANT at the core.

## Author config

Everything an author should tweak lives in the `CONFIG` block at the top
of the `<script type="module">` in `index.html`:

- `BOOK1_URL` — the Kindle store URL for Book 1.
- `NAMES` — the radio team voices, matched to Book One's resistance cell:
  `KARA` (leads the cell in the field), `THOMAS` (tactical — tracks machine
  patrols), `ELENA` (comms — monitors data streams and Marcus's vitals).
- `RADIO` — all 14 chatter lines, keyed by trigger.
- `INTRO_LINES` — the awakening sequence text.

## v1 scope (per spec)

- One weapon (pulse rifle, hitscan, infinite ammo, fire-rate cap)
- Two enemies: Crawler (melee rush) and Sentry (telegraphed ranged),
  three-state AI (idle → alert → attack) with line-of-sight triggers
- 100 HP with regen after 5s out of combat; checkpoints at segment doors
- Max 8 simultaneous active drones; all audio synthesized (WebAudio)
- All textures generated procedurally at load (canvas) — still zero assets
- Service workers are unregistered on load (caching fix)

Out of scope: squad NPCs, multiplayer, multiple weapons, saves, voice.
