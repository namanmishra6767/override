# OVERRIDE

A 10-stage, audio-first, top-down dungeon shooter that runs entirely in the browser. You are a rogue process injected into a live operating system, fighting your way down through directories to a final confrontation with **THE ROOT USER**. There are no image or video assets anywhere in the build — every visual is a canvas primitive and every sound is synthesized live with the Web Audio API.

**Play it:** `[ADD YOUR DEPLOYED URL HERE]` — see "Deploying" below, this needs one push.
**Repo:** `[ADD YOUR PUBLIC REPO URL HERE]`

---

## How to play

1. Click **INJECT PROCESS** on the title screen, put headphones on, and wait through the short boot/drop sequence (skip-proof by design — it sets up the audio context and is part of the intro).
2. **Move:** `WASD` or arrow keys. **Aim & fire:** mouse (hold left click to fire the current weapon at the cursor).
3. **Switch weapons:** `1` `PING_FLOOD` (fast, low-damage auto-blaster) · `2` `STACK_PUMP` (close-range shotgun with knockback) · `3` `MEM_CORRUPT` (short-range damage-over-time beam that also chews through walls' worth of enemies caught in its cone).
4. **Ultimates:** `SPACE` = `KERNEL_PANIC` (freezes enemy fire and enemies for a few seconds, complete with a low-pass-filtered, stuttering music glitch). `F` = `FORK_BOMB` (for 5 seconds, your shots that hit a wall split into two bouncing child projectiles). Both are on independent cooldowns shown bottom-right.
5. Walk over a glowing **Source Code Cache** to trigger a **Trade-Off Glitch** choice — every buff comes with a real hardware cost (bigger hitbox, slower movement, or double damage taken). Pick your poison.
6. Clear enemies (and the boss, on stages 3, 7, and 10) to open the green **Gateway Portal**, then walk into it to descend a level. Reach and purge the Root User on stage 10 to print `Process finished with exit code 0.`

On touch devices a virtual stick, fire button, weapon switcher, and ultimate buttons appear automatically.

---

## What this actually is

The uploaded document (`design-doc/OVERRIDE-blueprint.md` in this repo) was a conceptual pitch for a hackathon game — soundscape, level structure, weapons, and adaptive music, but no code. Everything playable was built from that brief in this session:

- A full canvas-based game loop (movement, collision, camera, particles, floating damage numbers).
- Procedural maze generation (randomized-DFS carve + courtyard punch-outs) for all 10 stages, regenerated fresh each run.
- 3 weapons, 3 stacking "glitch" trade-off upgrades, 2 ultimate abilities, grunt + turret enemies, and 3 distinct bosses (a gravity-well core, a firewall/turret gauntlet, and a weapon-disabling final boss).
- A from-scratch **adaptive music engine**: a 16th-note Web Audio scheduler drives a bassline that's always present, with drums and an arpeggio layer that fade in based on live "intensity" (nearby enemy count + boss state). `KERNEL_PANIC` drives the master lowpass filter down and slows the tempo for a submerged, stuttering effect, matching the original brief's "Exploit Swell" concept.
- The full pre-game audio-narrative intro (rain + accelerating mechanical-keyboard clacks synthesized from filtered noise bursts → sub-bass "BRAAM" drop with a swelling noise screech → silence + fan hum → text reveal) built as a scripted sequence over the audio engine.
- A CRT/scanline + vignette visual treatment, full HUD (health, score, per-weapon slots, ultimate cooldown bars, boss health bar, active-patch log), glitch-choice modal, and win/loss end screens, styled as a synthwave terminal.
- Mobile touch controls (virtual stick, fire button, weapon switcher, ultimate buttons) as a genuinely separate input path, not just a resize.

Nothing here is a template — there's no game engine, no starter kit, and no external audio/image libraries. It's vanilla HTML/CSS/JS in a single file, on purpose, so the "loads in under a second" claim from the original brief actually holds up.

## Build window

Built and QA'd in this session, in this order (see the trace zip for the real command-by-command log):

1. Read the design brief and decided on scope: a single-file HTML5 canvas game, since the brief's whole pitch was "no video/image assets, audio + text does the work."
2. Built the `AudioEngine` class first (noise buffers, oscillator voices, the scheduler-based adaptive music loop, the intro drop sequence) since it's the thing the brief cares about most.
3. Built maze generation, the player/enemy/projectile/collision simulation, the 10-stage config table, 3 bosses, the glitch-upgrade system, and the two ultimates.
4. Built the HUD, menus, glitch-choice modal, and win/loss screens, styled around a synthwave-terminal token system (near-black background, cyan/magenta/amber neon, monospace type) chosen to fit the subject rather than a generic template.
5. Added mobile touch controls as a first-class input path.
6. **Automated QA with Playwright** (headless Chromium) rather than eyeballing it: syntax-checked the extracted JS, then scripted a real playthrough — clicked start, waited through the boot sequence, drove movement/aim/fire/ultimates via synthetic input, force-loaded all 10 stage configs back-to-back to make sure every maze/boss combination initializes without throwing, forced the glitch-modal flow, forced a full boss-kill → victory-screen flow, forced a death → game-over-screen flow, and rendered the mobile viewport with touch controls. This caught one real bug — the boot sequence's async `setTimeout` chain didn't finish before test scripts assumed `player` existed — which pointed at genuinely loose timing in the intro; the intro delays were trimmed in response. Screenshots from these runs are included in the trace zip.

## AI tools used

- **Claude** (this conversation) — sole author of all design decisions, code, styling, and copy in this repo, driven from the user's one-line request ("build me a web game") plus the attached OVERRIDE blueprint document.
- **Playwright + headless Chromium** — used by Claude, inside the same session, as an automated QA harness (see above) to catch runtime errors before handing the build off, not as a design or code-generation tool.

No other AI tools, code generators, or asset generators were used.

## Prior work / external resources

- **Design brief only:** the file `design-doc/OVERRIDE-blueprint.md` (included) is the conceptual pitch that was supplied at the start of this session and used as the creative brief. It contains no code and no assets.
- **No game engine.** No Phaser/Unity/Godot/etc.
- **No external libraries, fonts, sound packs, or image assets.** All audio is synthesized at runtime with the Web Audio API (oscillators + a single procedurally-generated noise buffer); all visuals are canvas/SVG-free CSS + `<canvas>` 2D drawing. The page references a `JetBrains Mono`-style monospace stack but falls back to system monospace fonts — no font files are fetched.
- **No tutorials or copied code snippets.** The maze generator is a standard randomized-DFS carve algorithm (a well-known, uncopyrightable technique, implemented from scratch here) — flagged here for transparency even though it isn't "prior work" in the reuse sense.

## Known limitations / honest disclosures

- Enemy pathfinding is direct-line-with-wall-collision, not full A*, to keep the whole thing in one dependency-free file — it reads fine in a corridor shooter but isn't going to route around a complex dead end elegantly.
- The three bosses share a lot of underlying plumbing (shared `boss` object, per-kind behavior branches) rather than being fully separate classes — a deliberate scope cut for the time available.
- This environment could not push to a public git host or deploy to a live URL directly (no outbound network access in the build sandbox) — deploying and publishing the repo is the one step left for you, and it's a zero-build static file so it's genuinely one step. See below.

## Deploying (one step, no build tools needed)

This is a single static HTML file with zero dependencies and no build step.

- **GitHub Pages:** push `index.html` to a repo, enable Pages on the `main` branch root, done.
- **Netlify / Vercel:** drag-and-drop the `index.html` (or the whole folder) onto their web dashboard.
- **itch.io:** zip the folder and upload as an HTML5 project.

Then fill in the play URL and repo URL at the top of this README.

## File structure

```
index.html                     the entire game (HTML + CSS + JS, no build step)
design-doc/OVERRIDE-blueprint.md   the original creative brief this was built from
README.md                      this file
```
