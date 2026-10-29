# ANIMATION
ANIMATION
CLAUDE, THIS IF FOR YOU

## demo2 – procedural live music instrument
`demo2.html`: double-click it, then press **Start the instrument**. Press **?** to see the shortcuts.
7 mixable genres, 13 style flavors, live keyboard, sequencer, scenes, 3 themes, WAV and MIDI export.
Spec: `demo2-SPEC.md`.

### demo2 prompt (original, verbatim)

```text
You are a senior creative-coding engineer and sound designer. Build a
complete, modular, LIVE procedural music instrument for the browser.

════════════════════════════════════════
0. HARD CONSTRAINTS
════════════════════════════════════════
- Deliver ONE file: index.html (HTML + CSS + JS inline).
- No libraries, no npm, no build step, no CDN, no internet. Only the
  Web Audio API, Canvas 2D, and standard browser APIs.
- Must run by double-clicking the file in a modern browser on a
  Windows 10 laptop. The user is a total beginner, so the code must be
  heavily commented, with clear section headers.
- All sound is synthesized in real time. No audio samples.
- All melodies, riffs and progressions must be ORIGINAL. Use the
  artist references only as stylistic guidance (tempo, harmony, timbre,
  rhythm, arrangement habits), never to copy existing songs.
- Light CPU use by default, but the architecture must make it easy to
  upgrade later (see section 9).

════════════════════════════════════════
1. CONCEPT
════════════════════════════════════════
A live, endlessly evolving instrument that the user steers while it
plays. It covers 7 core GENRES, plus a separate STYLE-FLAVOR layer
inspired by artists. Genres can be MIXED together with on-board
controls.

Core genres: Techno, Psytrance, Hardbass, Blues, Rock, Jazz, Reggae.

Style flavors (each is a data preset that modifies tempo, scales,
timbre, rhythm habits, effects, and arrangement behavior):
- Astrix: full-on psytrance, 140-145 BPM, rolling bass, phrygian/minor
  melodies, squelchy filtered leads, long build-ups and breakdowns.
- Basshunter: eurodance / hands-up, ~138-145 BPM, bright supersaw
  leads, catchy simple hooks, sidechained pumping chords.
- Kino: Soviet post-punk / new wave, 100-130 BPM, minor keys, chorus-
  drenched clean guitar, drum-machine beat, melancholic dry bass.
- Scooter: hard dance / rave, 140-150 BPM, hard kick, rave stabs,
  pitched-up synth hooks, big builds with snare rolls.
- Rammstein: industrial metal, 90-125 BPM, palm-muted heavy distorted
  chugging riffs, stomping 4/4, dark minor/phrygian, brass/choir-like
  pad, aggressive dynamics.
- Clubbheadz: Polish club / electro house, ~126-130 BPM, punchy kick,
  rolling bass, catchy vocal-style synth hooks.
- Daft Punk: filtered disco-house, 110-125 BPM, heavy sidechain,
  funky chord stabs, phaser/filter sweeps, vocoder-style lead, 
  disco-influenced bass.
- Jean-Michel Jarre: analog synth soundscapes, 90-125 BPM, evolving
  sequencer arpeggios, warm pads, space-like reverb, melodic motifs.
- Kraftwerk: robotic electropop, 100-120 BPM, minimal strict sequences,
  clean synthetic percussion, simple memorable motifs, cold timbres.
- The xx: sparse minimal indie-electronic, 100-130 BPM, deep sub bass,
  reverb-soaked clean guitar-like plucks, lots of space, restrained
  drums.
- The Chainsmokers: melodic future-pop EDM, 95-105 BPM, plucky chord
  progressions, filtered drops, emotional major/minor hooks.
- Avicii: progressive house, ~125-128 BPM, uplifting major-key piano
  and pluck chords, folk-inspired lead hooks, euphoric build-and-drop.
- Deadmau5: progressive techno/house, ~126-128 BPM, long evolving
  builds, hypnotic arpeggios, deep detuned bass, patient arrangement.

════════════════════════════════════════
2. ARCHITECTURE (strict modules, each in its own commented section)
════════════════════════════════════════
A. Core engine: AudioContext, master chain (gain, compressor, limiter,
   analyser), lookahead scheduler (setInterval + currentTime), BPM,
   swing, time signature support, global transport (play/stop).
B. Seeded RNG (mulberry32 or similar). Same seed = same song.
C. Music theory module: scales (major, natural/harmonic minor, dorian,
   phrygian, mixolydian, pentatonic major/minor, blues, chromatic),
   chord builder (triads, 7ths, 9ths, sus, power chords), roman-numeral
   progression parser, key and transpose.
D. Instrument module. Every instrument has the same interface:
   trigger(time, note, velocity, params) and a params object.
   Include: kick (several types), snare, clap, closed/open hat, ride,
   rim, tom, noise riser, sub bass, acid bass, rolling psy bass,
   distorted bass, upright-style bass, pad, organ, electric piano,
   pluck, supersaw lead, square lead, guitar-style pluck, power-chord,
   palm-muted chug, arp synth, brass/choir-like pad, vocoder-style
   lead (formant filters).
E. Effects module (each as a reusable node wrapper): reverb (generated
   impulse response), feedback delay, distortion/waveshaper, bitcrusher,
   chorus, phaser, lowpass/highpass/bandpass filter with LFO, sidechain
   ducking, stereo widener.
F. Generator module: drumPattern(), bassline(), chordProgression(),
   melody(), arpeggio(), fill(), riser(). Each takes (genre data, style
   data, seed, energy) and returns plain pattern data (arrays of
   steps/notes), never plays sound directly. This separation is what
   makes everything editable.
G. Data module: ALL genres and style flavors defined as plain
   JavaScript objects at the top of the file (BPM range, swing, scales,
   progressions, drum rules, instrument list, effect chain, arrangement
   behavior). Adding a new genre must mean adding one object, with no
   other code changes. Put a short "HOW TO ADD A GENRE OR STYLE" guide
   in a comment at the top.
H. Arrangement module: sections (intro, groove, build, drop, breakdown,
   outro) with automatic or manual transitions, driven by an ENERGY
   value (0-100). Genres have their own arrangement habits (e.g.
   psytrance has long builds, blues is 12-bar cycles, jazz has head,
   solos, trading).
I. Mixer module: per-track volume, pan, mute, solo, send levels.
J. UI module (see section 5) and a Theme module (section 6).
K. Persistence module: presets, import/export.
L. Quality module (section 9).

════════════════════════════════════════
3. GENRE MIXING (important)
════════════════════════════════════════
- A "Genre Blend" panel with a weight slider (0-100) for each of the 7
  genres. Weights are normalized. The generators use the weights to
  blend: tempo (weighted average), scale choice, chord vocabulary,
  rhythm feel (straight vs swing vs shuffle), and instrument palette.
- A "Role Assignment" mode: pick a different genre for each role
  (drums from A, bass from B, harmony from C, lead from D). Example:
  reggae drums, psytrance bass, jazz chords, hardbass lead.
- A "Style Flavor" dropdown (or two flavors with a crossfade slider)
  layered over the genre blend.
- A "Chaos" slider that controls how much the blend randomly drifts
  over time, and a "Mutate" button for one-shot variation.
- Tempo handling: a "Tempo Lock" option and a half-time/double-time
  toggle so very different genres still fit together musically.
- Make sure mixed results still sound musical: force everything into
  one shared key/scale, and quantize everything to the shared grid.

════════════════════════════════════════
4. LIVE INSTRUMENT FEATURES
════════════════════════════════════════
- Computer keyboard as a piano (QWERTY rows) with octave shift,
  playing the currently selected lead instrument over the generated
  music, with an optional "snap to scale" toggle.
- XY pad (mouse/touch): X = filter cutoff, Y = resonance or effect
  amount (user-assignable).
- 8 MACRO knobs (user-assignable): Energy, Filter, Reverb, Delay,
  Distortion, Swing, Density, Brightness.
- Scene buttons: 8 scene slots that store the entire state and can be
  triggered live (with quantized switching on the next bar).
- One-shot performance buttons: Build-up, Drop, Breakdown, Fill,
  Stutter, Tape-stop, Riser, Reverse cymbal.
- Pattern editing while playing: a step sequencer grid (16/32 steps)
  per track plus a simple piano roll for melodic tracks. User edits
  are kept even when other tracks regenerate. Each track has a
  "lock" toggle (locked tracks are never regenerated) and a
  "regenerate this track only" button.

════════════════════════════════════════
5. UI (full control)
════════════════════════════════════════
Layout sections: Transport, Genre Blend, Role Assignment, Style Flavor,
Mixer, Macros + XY pad, Sequencer / Piano roll, Arrangement timeline,
Effects rack, Presets, Settings.
Controls: Play/Stop, BPM, key, scale, swing, seed (+ randomize), master
volume, energy.
Make it responsive for a laptop screen, and keyboard accessible.

════════════════════════════════════════
6. THREE SWITCHABLE THEMES (one-click switch, saved in settings)
════════════════════════════════════════
Implement themes with CSS variables plus a visual-mode switch, so the
same UI structure works for all three:
1) MINIMAL DARK: clean, flat, restrained colors, small waveform
   display.
2) VISUAL SHOW: reactive full-screen canvas visuals driven by the
   AnalyserNode (spectrum bars, waveform rings, particle bursts on
   kicks, color shifting with energy and genre blend), with the UI
   panels semi-transparent over it. Provide a "performance" setting
   to reduce visual load.
3) RETRO HARDWARE / 90s RAVE: skeuomorphic knobs and faders, LED
   step buttons, a tracker-style pattern view, neon rave palette,
   scanline/CRT option, pixel or monospace fonts.

════════════════════════════════════════
7. EXTRAS (all required)
════════════════════════════════════════
a) WAV export: record the master output in real time (or render
   offline with OfflineAudioContext) and download as .wav.
b) Presets: save/load full states (blend, style, patterns, macros,
   mixer, theme) in localStorage, and also export/import as a JSON
   file. Include several built-in demo presets.
c) Keyboard shortcuts: space = play/stop, 1-8 = scenes, M = mutate,
   R = regenerate, T = cycle theme, arrow keys = BPM/energy, plus a
   help overlay (press ?) listing all shortcuts.
d) MIDI export: export all tracks as a Standard MIDI File (.mid) with
   correct tempo, channels, drum channel 10, and note data (write the
   binary file format by hand, with no library).

════════════════════════════════════════
8. CODE QUALITY RULES
════════════════════════════════════════
- Start the AudioContext only after the first user click.
- No clicks or pops (use gain envelopes, short fades on start/stop).
- Disconnect and garbage-collect finished audio nodes; do not leak.
- Never create audio nodes inside tight loops without cleanup.
- Wrap risky code (localStorage, file export) in try/catch with
  friendly error messages in the UI.
- Consistent naming, small functions, JSDoc-style comments.
- A "Self-test" button that plays a short test pattern and logs
  results to a console panel, so a beginner can see if audio works.

════════════════════════════════════════
9. PERFORMANCE AND UPGRADE PATH
════════════════════════════════════════
- A QUALITY setting: Low (default), Medium, High. Low uses fewer
  voices, simpler oscillators, shorter reverb, and fewer visuals.
  Higher levels increase voice counts, add unison/detune, longer
  reverb, oversampling on distortion, and richer visuals.
- Keep ALL expensive features behind the quality setting, so future
  versions can add AudioWorklet-based DSP, sample support, or
  WebMIDI input without restructuring. Mark these spots with
  "// UPGRADE HOOK:" comments.
- Add a small CPU/voice-count monitor in the settings panel.

════════════════════════════════════════
10. HOW TO WORK
════════════════════════════════════════
1. First, give a short plan (module list, data structure outline, any
   risks). Do not write code yet.
2. Then build it in the following stages, and after each stage tell me
   exactly what to test and what to expect to hear and see:
   Stage 1: Engine, scheduler, RNG, theory, basic drums.
   Stage 2: Instruments, effects, bass and harmony generators.
   Stage 3: All 7 genres and 13 style flavors as data.
   Stage 4: Genre blend, role assignment, arrangement and energy.
   Stage 5: Live features (keyboard, XY pad, macros, scenes,
            sequencer, piano roll).
   Stage 6: UI, mixer and the three themes.
   Stage 7: Presets, WAV, MIDI, shortcuts, self-test, quality modes.
3. If the file gets too large for one reply, split the output into
   clearly labelled chunks that I can paste together in order, and
   tell me exactly where each chunk goes.
4. Whenever you make a design choice that I might want to change later
   (tempo ranges, scales, default instruments), put it in the DATA
   section, not inside the logic.
════════════════════════════════════════
VARIANT E OVERRIDES (these values replace any defaults above)
════════════════════════════════════════
- Global tempo: scale all genre and style BPM ranges by 0.94.
- Reverb tail length: 2.4 seconds (default). Low-quality mode may
  shorten it to 1.4s.
- Delay feedback default: 0.40.
- Chaos slider default: 24 (out of 100). The genre blend drifts
  slowly and smoothly over time, never in sudden jumps.
- Reverb and delay sends should be gently increased in breakdowns and
  reduced in drops.
- Keep Low quality as the default, so CPU use stays light despite the
  longer reverb. Mark the reverb length with "// UPGRADE HOOK:".
```
