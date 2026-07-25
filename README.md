# LATM: Hive Infiltration (v1)

Free playable episode set in the world of **Life After The Machines**.
Marcus wakes up inside a machine hive, fights through three corridor
segments, and plants a charge at the hive core. 5–7 minutes, then a
funnel to Book 1.

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
- Service workers are unregistered on load (caching fix)

Out of scope: squad NPCs, multiplayer, multiple weapons, saves, voice.
