# OVERRIDE // METROPOLIS

A high-stakes, browser-playable open-world stealth-action hacking district built inside a single dependency-free web framework. Infiltrate a completely re-engineered tactical city grid, dodge security drone vision cones, map acoustic profiles, and phase-walk through solid memory banks to subvert the sector core.

## 🔗 Submission Deliverables
* **Live Playable Game:** [INSERT YOUR DEPLOYED URL HERE]
* **Public Code Repository:** [https://github.com/namanmishra6767/override](https://github.com/namanmishra6767/override)
* **AI Build Traces & Logs:** Provided in the attached `override-ai-traces.zip` submission bundle.

---

## 🎮 How to Play

### Controls
* **Movement:** `W`, `A`, `S`, `D` (or Arrow Keys) to navigate wide city streets and corridors.
* **Aiming:** Move your mouse cursor to orient your hardware weapon's direction.
* **Fire / Neutralize:** Left-Click to discharge projectiles or execute a close-quarter stealth neutralization on un-alerted patrol drones.
* **Weapon Hot-Swaps:** * `1` — **PING_FLOOD [Covert]:** Low acoustic footprint, fast firing rate, lower damage profile.
  * `2` — **STACK_PUMP [Loud]:** Massive damage spread, heavy recoil shake, but generates a loud acoustic wave that alerts nearby grid sectors.
* **Tactical Ability:** * `G` — **Ghost Phase Walk:** Consume phase matrix energy to slide directly through solid skyscraper walls and slip behind enemy lines. *Warning:* Materializing inside a solid wall triggers a critical hardware failure and heavy damage penalty!
* **Pause / Settings Matrix:** Press `ESC` or `P` at any point to pause the local sub-grid simulation runtime environment, access active configuration controls, or restart the run.

### Objective
Infiltrate the sector map, locate the 4 high-value mainframe firewall nodes (`CORE_A`, `CORE_B`, `CORE_C`, `CORE_D`), and securely hack them by stepping into their interface boundaries. Override all four cores while maintaining structural integrity to liberate the network sector.

---

## 🛠️ What Was Built During the 24-Hour Window

Starting from nothing but a conceptual design blueprint, the entire code architecture was written, debugged, and optimized from scratch within the hackathon timeframe:

1. **Synthetic Neon Web Audio Pipeline:** Built entirely with native oscillator nodes and noise buffers. Features dynamic master volume configuration, real-time spatialized acoustic warning waves, and situational sound effects.
2. **Structured Grid Map Generator:** Uses a highly optimized City-Block Urban Grid layout. The generator enforces guaranteed transit avenues, carves interior tactical alleyways, creates centralized courtyard plazas, and safely clears the player's starting sector to prevent unfair spawn camps.
3. **Sliding-Collision Automated Enemy AI:** Programmed security drones with field-of-view (FOV) raycasting vision wedges. Drones move on smooth, clean corner-sliding movement loops through streets.
4. **Retro Terminal UI/HUD Layer:** Styled a cyberpunk-themed heads-up display showcasing real-time system alerts, current weapon holstering/equipping latency delays, and live animated canvas visual effects.
5. **Interactive Hardware Options Matrix:** Integrated an immediate Pause/Settings overlay providing live volume manipulation sliders, a CRT hardware screen line emulation toggle, and a camera screen-shake setting.

---

## 🤖 AI Tools & Trace Disclosures

* **AI Coding Agent:** This game was built using an autonomous agentic programming instance.
* **Autonomous Engineering Pass:** The build process utilized an internal simulation suite to actively launch, playtest, and programmatically drive the game loop using synthetic mouse, movement, and keypress signals to review performance parameters.
* **Real Bug Fix Trace:** During automation testing, a critical asynchronous timing exception was uncovered. The test metrics identified that the async introductory narrative text delays outlasted the default page timeout. The final product features optimized runtime sequence safety directly due to this automated QA telemetry.

*A complete chronological step-by-step log tracking all tool executions, script checkpoints, and screenshots generated during development is located in the `override-ai-traces.zip` submission.*

---

## 📝 Credits & Disclosures

* **Core Libraries & Engines:** None. The entire architecture is authored in standard, dependency-free vanilla HTML5, JavaScript Canvas API, and CSS3. 
* **Assets & Media:** Zero external audio files, image files, spritesheets, or fonts are used. Sound profiles are calculated dynamically via the Web Audio API, and all graphic styles are rendered programmatically via structural Canvas geometric drawing calls, ensuring a total payload footprint that initializes in milliseconds.
