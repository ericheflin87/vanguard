# VANGUARD Game Development — Complete Conversation Export

**Date:** June 15, 2026  
**Session Type:** Game design, narrative, and technical implementation  
**Status:** Chapter One complete (remastered), Chapter Two in progress (shooter mechanics)  

---

## 🎮 Project Overview

Building **VANGUARD** — an original, comedic military sci-fi narrative game inspired by the *tone* and *structure* of Halo's Fall of Reach arc, but with entirely original characters, story, and world.

**Format:** Narrative-driven 3D first-person shooter in the browser (Three.js)  
**Medium:** Single HTML file with Web Audio original score and real-time 3D graphics  
**Chapters:**
- **Chapter One:** "The Taking" — Childhood recruitment (narrative, no combat)
- **Chapter Two:** "Orientation (Armed)" — Live-fire training (playable shooter)
- **Chapter Three onwards:** "The First Contact (Unscheduled)" — TBD

---

## 📖 The Concept

### Why This, Not a Halo Clone?

Started with a user challenge: *"You can't do copyright infringement. Make it comically close in every way as a parody."*

**Key insight:** Parodying *Halo specifically* is indefensible. But parodying the *trope* — shadowy military program, stolen childhood, deadpan institutional satire — is both legal and more interesting.

**VANGUARD's angle:** A perfectly normal government initiative that recruits gifted children to train them as soldiers, then slowly reveals the *actual* reason they're needed. Tone is dark comedy mixed with dread. Story beats are original but echo the emotional arc.

### What Makes It Different

1. **Original score:** Fully composed in Web Audio (formant-filtered choir, taiko percussion, synthesized orchestral)
2. **Original world:** The Campus, a retrofuturistic military academy. Not Reach, not Earth.
3. **Original story:** Candidate 23's perspective. Opens comedic (posture survey, school shuttle with a cannon), pivots to ominous.
4. **Gameplay:** Escalates from narrative choice (Chapter One) to tactical FPS with enemy AI and weapon variety (Chapter Two+).

---

## 🎬 Chapter One: "The Taking" (Remastered)

### What Was Upgraded from Original

**Visuals:**
- Real-time soft shadows from directional sun
- Gradient dusk sky dome with 900 individually placed stars
- Twin moons (because one moon is for franchises with smaller budgets)
- Volumetric fog with depth cueing
- 240-particle dust burst on dropship landing with physics
- Fireflies drifting over playground grass
- Film grain, letterbox cinematic framing, vignette
- Stylized 3D rather than flat boxes (Three.js soft shadows, PBR materials)

**Audio (Original Composition):**
- Two-state music system: "wonder" (playground discovery) and "ominous" (ship arrival)
- **Wonder theme:** D-minor chord progression, formant-filtered choir pads (3-detuned sawtooths → lowpass + vocal bandpass for that "ahh" choir sound), plaintive melody with feedback delay
- **Ominous theme:** Detuned low drone with minor-2nd rub for dread, sparse taiko heartbeat, low choir pulses
- Smooth crossfades between states, swell transitions on scene changes
- Web Audio synthesis (no audio files, all procedural)

**Story (8 scenes):**
1. **Intro:** Narrator (much later) frames childhood as "very good at three things"
2. **Hill scene:** Player reaches hilltop, adults arrive (cinematic camera tween)
3. **Meeting:** Dr. Vess (lab coat) and Sgt. Brick (armor) introduce "routine posture survey"
4. **Reflex test:** Reaction-time catch game — branching dialogue based on performance (< 420ms = "exceptional," else = "adequate")
5. **Scholarship:** Vess explains the win
6. **The Taking:** Dropship descends with engine glow and beacon, narrator reflects
7. **Boarding:** Fade to black, interior switch, bunk hall reveal
8. **Ending:** Vess explains what VANGUARD is (training, purpose, "vaccines we are not legally required to count")

**Mechanics:**
- WASD + Mouse to move/look
- SPACE to advance dialogue
- 1/2 keys for dialogue choices
- M to toggle music
- Cinematic camera tweens during scripted moments
- Reaction-time test is a real interaction (player must wait, then catch on command)

**Technical:**
- Built with Three.js r128
- Compiled to single 41 KB HTML file
- Runs at 60fps on modern browsers
- Headphones required for full experience
- Responsive to window resize

---

## 🎯 Chapter Two: "Orientation (Armed)" — Shooter Build In Progress

### Design Goals

Transform the experience from narrative exploration to a **playable tactical shooter** while keeping the dark comedy tone and original music.

**Core Features:**
1. **Full FPS controls** — WASD movement, mouse look, jump, melee, reload
2. **Weapon system** — Carbine with magazine + reserve ammo, realistic ballistics
3. **Enemy AI** — Multiple enemy types with simple state machines (patrol → alert → attack)
4. **Wave-based combat** — Progressive difficulty, arena-based encounters
5. **Health/damage system** — HUD with integrity bar, knockback, visual/audio feedback
6. **Fully rebindable controls** — Custom keybinds persisted to localStorage
7. **Sensitivity + aim settings** — Look sensitivity slider, invert Y toggle, hold-to-aim option
8. **Original music state:** Combat transitions to ominous theme with faster taiko

### Control Scheme (Rebindable)

**Default Bindings:**
- **Movement:** W=Forward, S=Back, A=Left Strafe, D=Right Strafe
- **Jump:** Space
- **Sprint:** L-Shift
- **Fire:** Left Mouse
- **Aim:** Right Mouse (toggle or hold, configurable)
- **Reload:** R
- **Melee:** V

**Settings (Saved):**
- Look sensitivity: 0.3x to 3.0x (default 1.1x)
- Invert Y: On/Off
- Hold to aim: On/Off

**Control Menu:**
- Click "Controls" from title screen
- Each action shows current binding
- Click binding button to remap
- Press new key or mouse button to bind (ESC to cancel)
- "Reset Defaults" button to return to factory
- Bindings auto-save to browser localStorage

### Arena Design

**The Atrium** — Live-fire training facility at The Campus

**Layout:**
- 120m × 160m floor (grid-lined with emissive strips for visual interest)
- Walls at boundaries (cold geometry, no escape)
- Multiple cover objects (concrete blocks, pillars, crates)
- Spawn points: player starts center, enemies spawn at edges
- Dynamic lighting from ceiling panels

**Cover System:**
- Circular collision cylinders (for simplicity)
- Enemies pathfind around obstacles
- Bullets have simple raycast hit detection
- Melee has short range, requires facing enemy

### Enemy Types (Wave 1-3)

**"Drills"** — Basic training robots
- 1.8m tall, boxy frame
- Simple patrol → chase → shoot behavior
- Health: 20 HP
- Weapon: Low-accuracy burst fire
- SFX on death: descending pitch tone

**"Sparks"** — Faster, more aggressive
- 1.6m, leaner silhouette
- Dodge occasionally
- Health: 15 HP
- Weapon: Fast semiautomatic
- SFX on death: higher pitch than Drills

**"Sentries"** (Wave 3+) — Heavily armored
- 2.1m with visible armor plating
- Slow movement but high damage output
- Health: 40 HP
- Weapon: Heavy cannon (slower fire, high damage per shot)
- SFX on death: deep resonant tone

### Weapon Mechanics

**MR-7 "Paragon" Carbine** (starting weapon)
- Magazine: 24 rounds
- Reserve: 96 rounds (4 mags)
- Damage: 15 HP per shot
- Fire rate: 750 RPM (semiautomatic, ~10 shots/second max)
- Reload time: 2.2 seconds
- Accuracy: Tight spread, minimal recoil
- Melee damage: 30 HP per hit (swing with carbine stock)

**Ammo Management:**
- HUD shows current magazine / total reserves
- Auto-reload when mag empties (optional manual reload with R)
- Reload plays distinct sound (two-tone beep)
- Running low on ammo triggers warning text in HUD

**Future Weapons (Phase 2):**
- Plasma rifle (hitscan, energy-based)
- Rocket launcher (projectile, area damage)
- Sniper (slow fire, high damage, scope)

### Player Mechanics

**Health/Damage:**
- Start with 100 HP (Integrity)
- HUD bar shows health status
- Getting shot: knockback + screen flash + SFX
- Health pickups: Restore 25 HP (found in arena or dropped by enemies)
- Death: Restart drill (fade to black, respawn at start)

**Movement:**
- Walk speed: 7.5 m/s
- Sprint: 12 m/s (doubles movement)
- Jump: 5 m vertical (allows clearing obstacles, dodging)
- Air control: Full WASD control while airborne
- Footstep sounds: Subtle (would add in Phase 2)

**Combat Actions:**
- **Fire:** Hold or tap LMB, hitscan bullets with travel time
- **Reload:** Press R (2.2s animation)
- **Melee:** Press V, 30 HP per hit, 0.6s cooldown, immediate knockback
- **Aim (RMB):** Toggle or hold (configurable) for better accuracy

### HUD Elements

**Health Bar (bottom-left):**
- Label: "Integrity"
- Visual: Gradient bar (red → amber) showing health %
- Updates smoothly on damage
- Color intensity increases as health drops

**Ammo Counter (bottom-right):**
- Weapon name: "MR-7 'PARAGON' CARBINE"
- Magazine/Reserve: Large numbers, e.g. "24 / 96"
- Reload hint: Shows "RELOAD?" when mag empty
- Color codes: Amber for normal, red for low ammo

**Crosshair (center):**
- Simple dot + four lines
- Turns red on hit (hit feedback flash)
- Contracts/expands slightly based on accuracy (future: full bloom system)

**Objective Prompt (top-center):**
- Waves: "ELIMINATE WAVE 1 — ELIMINATE WAVE 2 — SURVIVE WAVE 3"
- Dynamic updates as waves change

### Audio (Combat Theme)

**Music Transition:**
- Wave 1 starts: "Wonder" theme fades out over 1.5s
- Ominous theme fades in: detuned drone, faster taiko
- Low choir pulses every 8 beats
- Tempo: ~120 BPM (faster than drill theme)

**SFX Catalog:**
- **Rifle shot:** Crisp snap (bandpass filtered noise + sine), 140ms
- **Melee swing:** Sawtooth sweep (420→120 Hz), 220ms
- **Reload:** Two-tone beep (200 Hz, 320 Hz), 180ms apart
- **Hit (player):** Sawtooth falling pitch (180→60 Hz), 280ms, 0.28 gain
- **Enemy death:** Type-dependent tone descents
- **Health pickup:** Rising chime (150→400 Hz triangle wave)
- **Wave complete:** Swell (choir pads + rising filter sweep)

### AI Behavior (Simple State Machine)

**Drill behavior:**
```
IDLE (patrol within spawn zone)
  ├─ If player visible & < 30m → ALERT
  └─ Random patrol every 3s

ALERT (moving toward player)
  ├─ If player in LOS & < 2m → MELEE (close-range attack)
  ├─ If player in LOS & 2-40m → FIRE (burst or semi)
  ├─ If line of sight breaks → SEARCH (2s looking around)
  └─ If not seen for 6s → IDLE

SEARCH (looking for player after LoS broken)
  ├─ If found again → ALERT
  └─ Timeout 6s → IDLE

MELEE (close combat)
  ├─ Attack every 0.8s while < 3m from player
  └─ Back away if player gets too close
```

**Pathfinding:**
- Enemies navigate around cover cylinders
- Simple grid-based steering (avoid colliders, move toward player)
- If blocked, try moving perpendicular to obstruction

### Wave Progression

**Wave 1: Training Drill**
- 3 Drills spawn in sequence (not simultaneously)
- Spawn every 4 seconds
- Weak, slow, good for learning controls
- Objective: Eliminate all 3

**Wave 2: Pressure**
- 5 Sparks spawn in pairs
- Spawn every 2.5 seconds
- Faster, more aggressive
- Forces player to move and use cover

**Wave 3: Endurance**
- 2 Sentries + 3 Sparks (mixed)
- Staggered spawns over 20 seconds
- High damage output, forces precision
- Complete = Chapter ends

### Game States & Flow

**Title Screen:**
- Logo + chapter title
- "Begin Live-Fire Training" button
- "Controls" button for rebinding
- Brief description

**Intro Cinematic (< 5s):**
- Fade from black
- Instructor voice: "Candidate 23, you have completed eight years of theory. This is your first live-fire evaluation."
- Fade to black
- Music swells

**Active Play:**
- Player spawns center of arena
- Wave 1 begins immediately
- HUD shows health + ammo
- Music is ominous state
- Real-time combat

**Between Waves:**
- 4-second pause
- Objective updates: "WAVE 2 INCOMING"
- Enemy count resets, player ammo not refilled
- Music holds ominous, slight intensity dip

**Death Screen:**
- Fade to black
- "Integrity Failure — Candidate Down"
- "The instructors note this on a clipboard." (flavor)
- "Restart Drill" button
- "Controls" button

**End Screen (all waves passed):**
- "Drill Complete — Orientation Passed"
- "Your reward is more orientation." (dark comedy)
- "Replay Chapter" button
- Teaser: "CHAPTER THREE: THE FIRST CONTACT (UNSCHEDULED) — IN PRODUCTION"

### Technical Implementation (In Progress)

**Language:** Three.js + Vanilla JavaScript (single HTML file)

**Key Systems:**
1. **Input Handler:** Listens for keydown/keyup, maps to actions via BINDS, populates `act` object
2. **Control Menu:** DOM-based, persists to localStorage
3. **Audio Engine:** Reuses Ch1 systems (choir, taiko, drone synthesis) + new SFX functions
4. **Physics:** Simple AABB/sphere collision, raycast bullet detection
5. **Enemy Manager:** Spawns waves, updates AI each frame, removes dead enemies
6. **HUD:** Updates ammo / health each frame, flashes on hit
7. **Game State Machine:** title → intro → play → wave2 → wave3 → end/death

**Performance Target:**
- 60 FPS on mid-range hardware
- < 100ms input latency
- Smooth at 1440p

**Browser Compatibility:**
- Chrome/Chromium (best)
- Firefox (good)
- Safari (limited — Web Audio may have quirks)
- Edge (good)

---

## 🔄 The Development Process

### Phase 1: Chapter One (Complete)
1. ✅ Concept & narrative structure
2. ✅ Original composition (Web Audio)
3. ✅ 3D world-building (Three.js)
4. ✅ Dialogue system
5. ✅ Cinematic camera tweens
6. ✅ Reaction-time game mechanic
7. ✅ Tested & deployed

### Phase 2: Chapter Two (In Progress)
1. ⏳ FPS controller (WASD + mouse look + jump)
2. ⏳ Weapon system (ammo, reload, fire)
3. ⏳ Enemy AI (patrol, chase, shoot)
4. ⏳ Wave system (progressive difficulty)
5. ⏳ HUD (health, ammo, objective)
6. ⏳ Control rebinding menu
7. ⏳ Audio SFX + music transitions
8. ⏳ Testing & balance

### Phase 3: Expansion (Planned)
- Additional enemies (5+ types)
- Secondary weapons (plasma, rocket, sniper)
- Environmental interactions (doors, platforms, vehicles)
- Chapter Three narrative (first alien encounter)
- Difficulty modes (Easy, Normal, Hard, Legendary)
- Leaderboard / score tracking (phase 4)

---

## 💡 Design Philosophy

### Why Browser-Based?

1. **Accessibility:** No installation, zero barrier to play
2. **Modularity:** Each chapter is self-contained HTML
3. **Iteration speed:** Reload and test in seconds
4. **Shareability:** Send a link
5. **Constraint breeds creativity:** Single file forces ruthless optimization

### Why Original Music?

- Web Audio synthesis is real-time and compact (no audio files)
- Procedural composition can evolve with game state
- It's part of the world-building (not a licensed track)
- Communicates tone: wonder → dread (thematic progression)

### Why Dark Comedy?

- Straight military sci-fi is saturated
- Satire lets us explore serious themes (childhood militarization, institutional authority) without heavyhandedness
- Humor makes the ominous moments land harder (tonal contrast)
- Players laugh, then feel uneasy (intended effect)

---

## 🎯 What's Next

### Immediate (This Session)
- [ ] Complete Chapter Two core gameplay loop
- [ ] Test combat balance (difficulty curve)
- [ ] Refine UI/UX (readability, feedback clarity)
- [ ] Polish audio (SFX variety, volume balance)

### Short-term (Next 1-2 weeks)
- [ ] Submit to Itch.io or similar for feedback
- [ ] Gather user playtesting data
- [ ] Iterate on wave difficulty
- [ ] Add difficulty selector to title screen

### Medium-term (Next month)
- [ ] Begin Chapter Three narrative
- [ ] Add 2-3 new weapons
- [ ] Implement environmental hazards
- [ ] Advanced enemy AI (team tactics, flanking)

### Long-term (Future)
- [ ] Full campaign (Chapters 1-5)
- [ ] Speedrun/challenge modes
- [ ] Co-op framework (future multiplayer?)
- [ ] Mod tools / custom level editor

---

## 📚 Reference: Technical Debt & Known Issues

### Phase 1 (Ch1) Issues (Resolved)
- ✅ Web Speech API fails in Obsidian Electron (N/A — this is a different project)
- ✅ Font rendering on different OS (font-family stack refined)
- ✅ Mobile responsiveness (responsive camera aspect)

### Phase 2 (Ch2) Open Issues
- ⚠️ Enemy spawning can overlap (add spawn point distancing)
- ⚠️ Melee range might feel imprecise (needs visual feedback, audio confirmation)
- ⚠️ Physics can feel "floaty" (may need gravity tuning)
- ⚠️ Audio context suspend on page load (mitigated with user gesture)

### Optimization Opportunities
- [ ] Culling (don't render enemies off-screen)
- [ ] LOD for distant objects
- [ ] Instancing for repetitive geometry
- [ ] Audio pool reuse (limit concurrent sounds)

---

## 🎮 How to Play (When Complete)

### Chapter One: The Taking
1. Open the HTML file
2. Click "Begin Memory Playback"
3. Use WASD to walk around playground
4. Click to look around (or use mouse if in pointer lock)
5. Reach the hill's summit to trigger the story
6. Follow on-screen prompts, use SPACE to advance dialogue
7. Use 1/2 to make choices when prompted
8. Sit back and experience the narrative

**Playtime:** ~8-10 minutes

### Chapter Two: Orientation (Armed)
1. Click "Begin Live-Fire Training"
2. Customize controls via "Controls" button if desired
3. Use WASD to move, mouse to aim
4. Click (left mouse) to fire carbine
5. Press Space to jump, V to melee, R to reload
6. Eliminate waves of enemies
7. Survive all 3 waves to complete the chapter

**Playtime:** ~12-15 minutes per run

**Difficulty:** Medium (designed for first playthrough clarity)

---

## 🏆 Success Criteria

**Chapter One:**
- ✅ Narrative is engaging and comedic
- ✅ Music enhances mood without distraction
- ✅ Graphics are stylistically cohesive
- ✅ Controls feel responsive
- ✅ Story branch based on reflex test works correctly

**Chapter Two (Target):**
- [ ] Combat feels fair and responsive
- [ ] Enemy AI is challenging but not unfair
- [ ] Control rebinding is intuitive
- [ ] HUD is clear and readable
- [ ] Music transitions feel organic
- [ ] 60 FPS sustained on target hardware
- [ ] All waves can be completed by skilled player
- [ ] Death/restart flow is smooth

---

## 🎬 Narrative Arc (Full Campaign Vision)

**Chapter One: The Taking** ✅ Complete
- Age 6, playground recruitment
- Innocent discovery, growing dread
- Ends: boarding the dropship, loss of childhood

**Chapter Two: Orientation (Armed)** ⏳ In Progress
- Age 14, live-fire training
- First real combat, pushing boundaries
- Ends: Completion of training evaluation, hinted at larger purpose

**Chapter Three: First Contact (Unscheduled)**
- Age 17, first real deployment
- Encounter with what VANGUARD was actually training to fight
- Shift from military satire to existential dread

**Chapter Four+: The War** (Planned)
- Age 20-30, escalating conflict
- Questions about loyalty, free will, survival
- Series concludes with moral reckoning

---

## 📞 Design Decisions Explained

### Why Single HTML File?

**Pros:**
- Distributable via link (no CDN required)
- No build step (easier for iteration)
- All dependencies bundled (Three.js from CDN, Web Audio native)
- Forces clean architecture (no file dependencies)

**Cons:**
- File size grows (currently ~41 KB for Ch1, ~80 KB target for Ch2)
- Monolithic code (harder to refactor later)
- Testing is manual (no unit test framework)

### Why Web Audio Over Audio Files?

**Pros:**
- Compact (synthesized music ≠ MP3 files)
- Dynamic (music can be procedurally generated, responsive to game state)
- No loading delays
- Real-time parameter modulation

**Cons:**
- Limited sample replay (no recorded instruments)
- More CPU on older devices
- Steeper learning curve (synthesis vs. audio editing)

### Why Parody, Not Clone?

**Legal:**
- Fair use is murky; parodying a franchise beats parodying a trope
- Original characters, story, world protect from copyright claims

**Creative:**
- Trope-level satire is more timeless
- Frees us to explore themes (militarized childhood) without franchise baggage
- Funnier because less expected

### Why This Tone (Dark Comedy)?

**Emotional arc:**
- Opens light (playground, posture survey) → player is off-guard
- Closes ominous (ship, facility) → tonal gut-punch
- Combat gameplay reinforces dread (what are we training for?)

**Thematic:**
- Satire of militarism, institutional power
- Childhood stolen for greater good (questionable)
- Questions whether the audience is complicit (playing the soldier)

---

## 🔗 Resources & Dependencies

**Three.js r128**
- Latest stable version for this era
- Soft shadows, PBR materials, fog, instancing all available
- CDN: `https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`

**Web Audio API**
- Native browser API, no external dependency
- Supported in Chrome, Firefox, Safari, Edge
- Synthesis functions are browser-compatible

**LocalStorage**
- Browser-native key-value store
- Used for control bindings and settings
- Max 5-10 MB (sufficient for our use)

---

## 📋 Checklist: What's Needed for Full Ch2 Release

- [ ] FPS controller (input + physics + camera)
- [ ] Weapon system (ammo, reload, fire detection)
- [ ] Enemy AI (at least 1 type working)
- [ ] Wave spawner (all 3 waves spawning correctly)
- [ ] Collision detection (enemies, bullets, cover)
- [ ] Health / damage system
- [ ] HUD (health bar, ammo counter)
- [ ] Sound FX (5+ event sounds)
- [ ] Music transitions (drill → combat)
- [ ] Control rebinding menu (fully functional)
- [ ] Death / restart flow
- [ ] End screen & pass condition
- [ ] Balance testing (difficulty curve)
- [ ] Polish & optimization
- [ ] Browser testing (Chrome, Firefox, Safari)

---

## 🎓 Lessons from Development So Far

1. **Web Audio is powerful** — Procedural music saves bandwidth and adds dynamic depth
2. **Cinematic framing matters** — Letterbox, vignette, grain elevate presentation dramatically
3. **Narrative + gameplay** — Game doesn't need to be pure mechanics; hybrid narrative-gameplay layers experiences
4. **Constraint breeds creativity** — Single HTML file forces ruthless prioritization (no bloat)
5. **Parody works because it's earned** — Comedy lands only if the audience trusts the game has real stakes behind it

---

## 🚀 Final Notes

This project combines:
- **Narrative depth** (character, dialogue, thematic intent)
- **Technical ambition** (real-time 3D, Web Audio synthesis, AI)
- **Artistic cohesion** (music, visuals, tone all aligned)
- **Accessibility** (zero installation, runs in browser, keyboard-friendly)

The result is a game that feels cinematic and complete, despite being delivered as a single HTML file.

Next steps are tactical: finish the combat loop, test with players, iterate, and move toward Chapter Three.

---

**End of conversation export. All major decisions, technical details, and design philosophy documented for continuity across sessions.**

**Session concluded:** June 15, 2026, ~3 hours of development discussion and 1 hour of implementation.
