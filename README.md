# Echo Loop

A top-down survival browser game, Vampire-Survivors-style, with a twist: when you
die, your last life is recorded and replays forever as a "ghost" that fights
alongside you. Ghosts accumulate across deaths and get progressively stronger
the more of them there are.

## Play

Open `echo-loop-survival.html` directly in a browser — it's a single
self-contained file (canvas 2D, no build step, no external assets, no server
required), so it also works fully offline and is a natural candidate for
wrapping in Electron/Tauri/nw.js later to ship as a downloadable desktop app.

**Controls:** WASD to move, J to attack, R to fully reset the run.

## How it works

- You level up during a life by killing enemies (slimes → bats → brutes as
  difficulty ramps).
- Enemy HP scales with total elapsed survival time, uncapped by design — no
  ghost army lets you out-scale it forever.
- Each ghost's strength depends only on how many ghosts already exist
  (death order), not on the level you happened to reach that life — so early
  ghosts are weak and later ones carry hard. This is shown visually: ghosts
  are the player sprite recolored grey → gold as their power increases.
- All sprites are procedurally generated at load time from math-defined
  masks + shading functions (see `buildSprite()` / `SPRITES` in the source),
  not hand-drawn pixel art.

## Known next steps

- Touch controls (virtual joystick + attack button) for mobile.
- Responsive canvas sizing (currently a fixed 700x480).
- Deciding whether ghosts should eventually cap or expire.
