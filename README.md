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

**Flow:** Title screen → Enter → main menu (Start / Upgrades). **In-game
controls:** WASD to move, J to attack, R to abandon the current run and
return to the menu.

## How it works

- You level up during a life by killing enemies (slimes → bats → brutes as
  the threat tier climbs).
- **Difficulty resets every death and ramps by numbers, not HP.** Each life
  starts back at threat tier 0. Every 15-30 seconds the tier steps up,
  spawning enemies faster and in bigger batches (never with more HP) — by
  the later tiers of a long life the screen is meant to be nearly full of
  mobs you have to out-maneuver with upgraded speed and attack range.
- **Ghosts soak targeting.** Every enemy chases whichever is nearest, you
  or a ghost — so as echoes pile up across deaths, they pull swarm
  attention away from you and buy you room to survive the early tiers of
  each fresh life. Contact damage still only ever affects the real player.
- Each ghost's strength depends only on how many ghosts already exist
  (death order), not on the level you happened to reach that life — so early
  ghosts are weak and later ones carry hard. This is shown visually: ghosts
  are the player sprite recolored grey → gold as their power increases.
- All sprites are procedurally generated at load time from math-defined
  masks + shading functions (see `buildSprite()` / `SPRITES` in the source),
  not hand-drawn pixel art.

## Meta-progression

- Monsters have a 1% chance to drop a gold coin on death; walk over it to
  collect. An uncollected coin sits forever until you either pick it up or
  die — dying (not just returning to the menu) clears whatever's still on
  the ground. Gold you've actually banked is permanent and saved to
  `localStorage`, independent of runs, deaths, or resets.
- Spend gold in the Upgrades menu on permanent, run-independent boosts
  (starting attack, starting max HP, movement speed %, experience gain %).
  "Respec" fully refunds gold spent on upgrades so you can reallocate it —
  it never destroys gold you've earned.

## Known next steps

- Touch controls (virtual joystick + attack button) for mobile.
- Responsive canvas sizing (currently a fixed 700x480).
- Deciding whether ghosts should eventually cap or expire.
- Expanding the upgrade list beyond the current starter set.
