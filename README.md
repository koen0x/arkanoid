# Arkanoid

A standalone browser reconstruction of **Taito's 1986 Arkanoid**, built as a
single self-contained HTML file:

```text
arkanoid.html
```

Open the file directly in a modern browser. Runtime use requires no installer,
package manager, web server, framework, CDN, external asset, or network
connection.

## Project status

The project is functionally complete and is maintained as a v1.0-quality
reconstruction. It preserves the source engine's game feel while adding
evidence-based arcade content and isolated browser tooling.

Current gameplay includes:

- Rounds 1-32 with compressed 13 × 25 stage data.
- The dedicated Round 33 / DOH boss sequence.
- Normal, Silver, and Gold bricks.
- L / E / C / S / D / P power-ups plus B / Break and its exit portal.
- Multiball, Laser, Catch, Expand, Slow, Extra Life, enemies, and top doors.
- Embedded PC-88 audio with lazy decoding, overlap, mute, and gesture unlock.
- Fixed 60 Hz simulation and responsive 600 × 800 presentation.
- Original arcade-style repeating playfield textures: Blue, Green, Maze, Red,
  and the Round 33 DOH/orange field.
- Optional controller-only autoplay using the normal paddle and action paths.
- Attract/demo mode after 10 seconds of title-screen inactivity. It selects
  only normal rounds, runs for at most 60 seconds, and does not alter player
  high-score data.
- True browser fullscreen and scaled pointer input.

The runtime remains a single HTML file; repository assets and tools support
development and verification but are not required to launch the game.

## Canonical target and evidence

The primary arcade target is **Arkanoid (US, newer)**, MAME set `arkanoidu`,
associated with Taito / Romstar. Evidence is ranked as follows:

1. Direct `arkanoidu` / MAME arcade evidence.
2. Independently confirmed arcade behavior.
3. Original Taito MSX disassembly as fallback evidence.
4. Explicit deterministic reconstruction where stronger evidence is absent.

MSX, remake, and inferred behavior is labelled as such rather than presented
as proof of arcade behavior. See [SOURCES.md](SOURCES.md).

## Controls

Normal play:

- **Left / Right Arrow** or **mouse/pointer**: move Vaus.
- **Space** or **click**: contextual action, including ball release and Laser.
- **M**: toggle audio mute. The preference is stored under
  `arkanoid.settings.v1`.
- **F**: toggle true browser fullscreen. Browser Escape exits fullscreen.
- **A**: toggle autoplay during play. From the title screen it starts the
  selected round, or Round 1 when no round is entered.
- On the title screen, type **1-33** and press Enter to select a round. The
  title prompt advertises the normal range as 1-32; entering 33 directly starts
  the DOH round. Space starts Round 1.

Debug Lab controls are available only when DEBUG is enabled:

- **D**: show or inspect the diagnostics/timeline tools.
- **B**: open Ball Test for a stored frame.
- **P**: cycle the autoplay paddle-contact zone lock.
- **T**: select or disable an autoplay target point and optional trajectory.
- **J**: export the available diagnostic/timeline data.
- **Left / Right Arrow**, with **Shift** for a 60-frame step: review timeline
  frames when the inspector is active.
- **[ / ]**: reduce or increase simulation speed; **\\**: return to 1×.

The former manual incident-key UI is no longer a player control. Internal
bookmark support remains available to the diagnostic implementation and
exports.

## Diagnostics and engineering quality

The Debug Lab records fixed-step state, collision events, autoplay decisions,
and reviewable full-level timelines without rewinding or resimulating live
gameplay. P/T locks are controller constraints only: they do not add angles or
change collision physics. Ball Test works from captured state and reports
placement and aiming validity without changing normal play.

The source-backed regression suite loads the actual inline script in a Node VM
and covers physics, collision fidelity, autoplay, P/T locks, Ball Test,
DebugTimeline, audio, fullscreen, attract mode, backgrounds, and Round 33.
Focused examples:

```sh
node tests/physics-bounce-test.js
node tests/collision-fidelity-test.js
node tests/autoplay-debug-locks-test.js
node tests/debug-timeline-test.js
node tests/round33-doh-test.js
```

The simulation remains fixed at 60 Hz regardless of rendering or debug speed.

## Power-ups and Break

| Capsule | Name | Status |
|---|---|---|
| L | Laser | Implemented |
| E | Expand | Implemented |
| C | Catch | Implemented |
| S | Slow | Implemented |
| B | Break | Implemented |
| D | Disruption / Duplicate | Implemented |
| P | Extra Life | Implemented |

Effects use independent gameplay state where required. Break opens the right
portal, allows normal gameplay to continue, and completes through the existing
portal-exit lifecycle; it does not immediately end the round.

## Playfield backgrounds

Rounds 1-32 use the repeating arcade texture cycle Blue, Green, Maze, Red.
Round 33 uses the DOH/orange texture. The textures are clipped to the interior
playfield and rendered with crisp nearest-neighbor behavior beneath the game
objects. Extraction sources and licensing cautions are documented in
[ASSETS_AND_LICENSING.md](ASSETS_AND_LICENSING.md) and [SOURCES.md](SOURCES.md).

## Stage data and Round 33

Rounds 1-32 use reconstructed arcade-style layouts cross-checked against
reference maps. The project does not claim that these layouts are ROM-
fingerprinted `arkanoidu` data.

Round 33 is a separate DOH subsystem with registered arcade-derived sprite
assets, fixed projectile behavior, hit scoring, defeat animation, and dedicated
audio. Its lifecycle is intentionally separate from the regular brick-stage
system. Round 33 is excluded from attract/demo selection.

## High score and distribution

High score persistence uses:

```text
localStorage["arkanoid.highScore"]
```

Storage failures do not prevent play. The intended public artifact remains a
single `arkanoid.html` containing inline JavaScript/CSS and embedded runtime
images, fonts, and audio. Development tools and source assets remain outside
the runtime dependency path.

The code lineage, fonts, graphics, level data, audio, and research sources do
not necessarily share one license. Review
[ASSETS_AND_LICENSING.md](ASSETS_AND_LICENSING.md) before redistribution.

## Documentation

- [DEVELOPMENT.md](DEVELOPMENT.md): architecture, lifecycle, mechanics, and
  stable-system decisions.
- [PHYSICS_DIAGNOSTICS.md](PHYSICS_DIAGNOSTICS.md): detailed physics,
  diagnostics, autoplay, DebugTimeline, and debug-tool reference.
- [SOURCES.md](SOURCES.md): evidence, provenance, and confidence labels.
- [ASSETS_AND_LICENSING.md](ASSETS_AND_LICENSING.md): asset inventory and
  licensing cautions.
- [AGENTS.md](AGENTS.md): maintenance guidance for future agents.

Historical planning material is retained in
[archive/ROADMAP.md](archive/ROADMAP.md) and
[archive/ARKANOID_CODEX_PORT_PROMPT.md](archive/ARKANOID_CODEX_PORT_PROMPT.md).

## Attribution

Arkanoid was created by **Taito Corporation** in 1986. This project is an
independent, non-commercial reconstruction/porting project and is not
affiliated with or endorsed by Taito.
