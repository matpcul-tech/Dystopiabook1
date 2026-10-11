# LATM: Hive Infiltration

Free playable episodes set in the world of **Life After The Machines**,
funneling players to Book 1.

- **Chapter 1, The Hive**: Marcus wakes inside a machine hive, fights
  through three corridor segments, and plants a charge at the core.
- **Chapter 2, The Processing Center** (`#ch2`): armed from the start,
  Marcus crosses the cylinder halls from the book, including cylinder
  A-113, ANGELA M., and pulls the ledger of taken names while wardens
  (heavy sentry frames) defend the control room.
- **Chapter 3, The Final Upload** (`#ch3`): the finale. Fight through
  the pre-war mountain research facility (vehicle bay, research wing,
  warden-guarded power hall) to the uplink lab, then hold at the neural
  interface for the upload while everything the machines have converges.

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

- `BOOK1_URL`, the Kindle store URL for Book 1.
- `NAMES`, the radio team voices, matched to Book One's resistance cell:
  `KARA` (leads the cell in the field), `THOMAS` (tactical, tracks machine
  patrols), `ELENA` (comms, monitors data streams and Marcus's vitals).
- `RADIO`, all 14 chatter lines, keyed by trigger.
- `INTRO_LINES`, the awakening sequence text.

## v1 scope (per spec)

- One weapon (pulse rifle, hitscan, infinite ammo, fire-rate cap)
- Two enemies: Crawler (melee rush) and Sentry (telegraphed ranged),
  three-state AI (idle → alert → attack) with line-of-sight triggers
- 100 HP with regen after 5s out of combat; checkpoints at segment doors
- Max 8 simultaneous active drones; all audio synthesized (WebAudio)
- All textures generated procedurally at load (canvas), still zero assets
- Service workers are unregistered on load (caching fix)

Out of scope: squad NPCs, multiplayer, multiple weapons, saves, voice.

## Graphics (modern look)

The renderer was upgraded from a flat retro look to a gritty, cinematic one while
keeping the same single-file, no-build architecture and the same gameplay.

- **Materials:** every wall, floor, ceiling, door and crate uses procedural PBR
  textures generated on a canvas at load (albedo, normal map derived from a painted
  height map, packed roughness and metalness, emissive). Hex plating, louvered vents
  with light leaking through, hazard bands, wet patches and bolt detail. No image assets.
- **Lighting:** cold ambient, a shadow-casting helmet flashlight (high tier), an omni
  headlamp, a coloured accent light that hops between ceiling fixtures, muzzle flash light
  and the objective glow. Light shafts, drifting dust, glow halos at fixtures, flowing
  conduits. World-space ambient occlusion and wet-floor roughness are done in shader.
- **Reflections:** `sky.jpg` plus machine light panels are baked into a PMREM
  environment map, so steel and wet floor mirror the hive lights.
- **Post:** ACES filmic tone mapping, bloom, FXAA, split-tone color grade per chapter,
  vignette, film grain, chromatic aberration that spikes on hits, desaturation at low health.
- **Combat feel:** viewmodel recoil, sway and bob, muzzle flash sprite, ejected brass,
  tracers, pooled spark particles, bullet scorch decals, enemy hit flashes and eye halos,
  death bursts, hit markers, directional damage indicator, camera kick and roll.
- **HUD:** minimal ring gauges, thin crosshair that opens on fire, objective marker,
  restyled radio feed, touch controls and title screens.

### Quality tiers

| Tier | Intended for | What it does |
|------|--------------|--------------|
| low  | phones, weak GPUs | direct render (no post), pixel ratio capped at 1.15, no shadows, 80 dust motes, 4 light shafts, 256px textures |
| med  | mid laptops, phones that are coasting | bloom + color grade, pixel ratio 1.35, no shadows |
| high | desktops | shadow-casting flashlight, FXAA, pixel ratio up to 1.75, full particle counts |

The tier is picked automatically (touch phones start on low, small or old desktops on
med, everything else on high). A governor measures fps while playing: two bad 2.5 second
windows in a row step the tier down (remembered on the device), and a phone that holds
57+ fps for three windows is promoted one tier, once. As a last resort on low it renders
at fewer pixels. Override with `?q=low|med|high` or the GRAPHICS button on the title screen
(AUTO, LOW, MED, HIGH).
