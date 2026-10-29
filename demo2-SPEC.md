# demo2 – spec (Variant E)

The original brief that `demo2.html` was built from, summarised.

**Role:** senior creative-coding engineer and sound designer. **Build:** a complete, modular, live procedural music instrument for the browser.

## Hard constraints
- One self-contained HTML file. No libraries, npm, build step, CDN or internet. Only Web Audio, Canvas 2D and standard browser APIs.
- Runs by double-clicking on a Windows 10 laptop. Heavily commented for a total beginner.
- All sound is synthesized live (no samples). All melodies, riffs and progressions are original. Artists are only stylistic references.
- Light CPU use by default, with an easy upgrade path.

## Concept
7 core genres (Techno, Psytrance, Hardbass, Blues, Rock, Jazz, Reggae) that can be mixed, plus 13 artist-inspired **style flavors**: Astrix, Basshunter, Kino, Scooter, Rammstein, Clubbheadz, Daft Punk, Jean-Michel Jarre, Kraftwerk, The xx, The Chainsmokers, Avicii, Deadmau5.

## Architecture (modules)
A core engine + lookahead scheduler · B seeded RNG · C music theory · D instruments (one shared `trigger(time, note, velocity, params)` interface) · E effects · F generators (return plain pattern data only) · G data (all genres/styles as plain objects, plus a "how to add a genre" guide) · H arrangement + energy · I mixer · J UI + themes · K persistence · L quality.

## Genre mixing
Blend weight sliders, per-role genre assignment, style flavor A/B crossfade, chaos drift + Mutate, tempo lock, half/double-time, shared key/scale and grid.

## Live features
QWERTY piano with snap-to-scale, XY pad, 8 assignable macros, 8 quantized scenes, one-shots (Build-up, Drop, Breakdown, Fill, Stutter, Tape-stop, Riser, Reverse cymbal), step sequencer + piano roll with per-track lock/regenerate.

## UI and themes
Transport, blend, roles, style, mixer, macros/XY, sequencer, timeline, FX rack, presets, settings. Three themes: Minimal dark, Visual show (reactive full-screen canvas), Retro 90s rave (knobs, LEDs, tracker view, CRT scanlines).

## Extras
WAV export, presets (localStorage + JSON import/export + built-in demos), keyboard shortcuts with a `?` help overlay, hand-written Standard MIDI File export (drums on channel 10).

## Code quality and performance
Audio starts only on a click, no clicks/pops, nodes cleaned up, try/catch around storage and export, a self-test button with an on-screen log. Quality Low (default) / Medium / High, `// UPGRADE HOOK:` markers, CPU/voice monitor.

## Variant E overrides
- All genre and style BPM ranges × **0.94**
- Reverb tail **2.4 s** (Low quality may use 1.4 s), marked `// UPGRADE HOOK:`
- Delay feedback default **0.40**
- Chaos default **24**; the blend drifts slowly and smoothly, never in jumps
- Reverb/delay sends go up in breakdowns and down in drops
- Low quality stays the default
