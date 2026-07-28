# Snake & Candy — Roadmap

**Every idea on the original list is now built.** Nothing is uploaded yet.

> 📌 **Upload this file to your GitHub repo** (same place as `index.html`).
> Then it lives with the project forever, and next time we work together I can
> read it straight from the repo and pick up exactly where we left off.

---

## ✅ Built and waiting to go live

**The original game**

- Snake eats candy, score goes up
- 1 player · 2 player same device · 2 player online with a room code
- On-screen arrow buttons

**Round 1 — controls and looks**

- **Swipe to steer** — up, down, left, right, anywhere on the board
- **Four speed levels**: 🐌 Easy · 🙂 Medium · 🔥 Hard · 💀 Insane (Easy is the default)
- **Arrow buttons beside the board** on iPads and laptops, so nothing scrolls
- **Realistic snake** — one smooth connected body, tail tapering to a point,
  eyes facing the way you're going, a flicking tongue, X eyes when you crash,
  and it **glides** between squares instead of jumping
- **Bigger map**
- Pause overlay, gently pulsing fruit

**Round 2 — many players**

- **Up to 6 players online.** Lobby with a room code; everyone gathers, the host
  presses Start
- **The board grows with the crowd** — 30×30 for 1–2 players, 36×36 for 3–4,
  40×40 for 5–6
- Scoreboard across the top; final standings with a 👑 for the winner
- Last snake alive wins. If everyone crashes together, highest score wins

**Round 3 — fruit and colours**

- **Five kinds of fruit**, several on the board at once (3, plus one per player)

  | Fruit | What it does |
  |---|---|
  | 🍬 Candy | +10 points, grow by 1 |
  | 🍒 Cherry | +25 points, rarer |
  | 🍌 Banana | Shrinks you by 3 — an escape hatch when you're huge |
  | ⚡ Lightning | You move ~1.8× faster for 5 seconds |
  | ❄️ Ice | Slows *everyone else* to ~0.55× for 5 seconds |

- **Pick your own colour** — 6 to choose from, taken ones grey out
- **Your name** on the scoreboard
- Snakes glow while a power-up is active, so you can see who's affected

**🏆 Path of Prey — reward track**

Rewards unlock as your **total score across every game ever** climbs. Twelve
rewards in total. Progress is saved on your device and never resets.

The first ten alternate skin/trail, so you get something new every 100 points
rather than waiting ages for the first trail. Then there's a long gap to the
**legendary** pair. They're **separate slots** — you can wear Hulk with a
rainbow trail, or the Hacker skin with the Hacker trail once you've earned both.

| Points | Reward | Kind | Look |
|---|---|---|---|
| 100 | ⚡ Lightning Trail | Trail | Forked bolts with a white-hot core and blue halo, flickering |
| 200 | 🤖 Iron Man | Skin | Red and gold, pulsing arc reactor on the head |
| 300 | 🌈 Rainbow Trail | Trail | One continuous glowing ribbon, colour shifting along it |
| 400 | 🔨 Thor | Skin | Silver and blue, lightning bolt on the head |
| 500 | ☠️ Poison Trail | Trail | Gas clouds that billow outward, fade in fast and out slow |
| 600 | 🕷️ Spider-Man | Skin | Red with dark blue webbing across the body |
| 700 | 💨 Dirt Trail | Trail | Clods + fine dust sprayed backward, tumbling and settling |
| 800 | 💚 Hulk | Skin | Green with purple bands, drawn 18% chunkier |
| 900 | 🦸 Superman | Skin | Blue and red with a diamond emblem |
| 1000 | 🐜 Ant-Man | Skin | Dark red, drawn at 66% size — genuinely tiny |
| **2750** | 💻 **Hacker Trail** | Trail | 🟢 **LEGENDARY** — streams of code shed off the tail, every glyph re-rolling as it fades |
| **3000** | 💻 **Hacker** | Skin | 🟢 **LEGENDARY** — near-black body, neon green, a terminal screen on the head with a blinking cursor |

**Classic** skin and **No Trail** are free from the start.

Notes:

- **Trails are cosmetic. Skins are not any more** — six of them carry an
  ability (see below). Ant-Man's *passive* look is still cosmetic; he only
  actually phases while SHRINK is active.
- Trails are drawn from each device's own copy of the game, so they cost
  **nothing** in network traffic even with six players.
- Particles are capped at 80 per snake and expire on a timer, so they can't pile
  up and slow the game down. Measured steady state: lightning 6, rainbow 35,
  poison 38, dirt 57, hacker 39.
- The Hacker **skin** uses the key `hacker`; the Hacker **trail** uses
  `hackertrail`. They must not share a key — skins and trails are looked up
  separately today, but one id meaning two things is a trap.
- **The physics is top-down.** An early version had dirt falling and poison
  rising, which looked wrong because the camera looks straight *down* at the
  board — there is no "down" on screen for things to fall toward. Dirt now
  sprays backward from the tail and skids to a halt with friction; poison
  spreads outward like a real cloud.
- Several players can wear the same skin online. Your chosen colour is drawn as
  an **aura around your snake** so you can always find yourself.
- In same-device 2P the **better** of the two scores counts. Online, only your
  own snake's score counts — not the winner's.
- **Pacing** (simulated): first reward in game 1–3, Ant-Man around game 13–20,
  then a long climb — the Hacker pair lands somewhere around game **25–60**
  depending on how well you score. That gap is deliberate: it's the legendary
  tier. If it feels too far, lower the two `unlockAt` numbers.
- The first ten rewards sit on a neat 100-point grid; the legendary two do not
  (2750 and 3000). The progress bar measures from the **last reward you passed
  to the next one**, so it fills smoothly across the big gap instead of sitting
  full for twenty games.
- ⚠️ The hero names are trademarks of Marvel and DC. Fine for a personal
  project. To change them, edit the `name` fields in the `SKINS` list near the
  top of the file — nothing else depends on them.

### ⚡ Skin abilities

Six skins now have a power. One button under the board (or press **H**), and
**every ability shares a 15 second cooldown**.

| Skin | Ability | What it does |
|---|---|---|
| 🔨 Thor | **HAMMER** | A hammer orbits your head for 3.5s at 2.6 squares out. Any snake whose head enters its 3×3 zone dies. Never hurts you. |
| 🔆 Iron Man | **LASER** | Instant beam straight ahead, up to 12 squares. Kills the **first** snake it touches, then stops — no wiping a whole row. |
| 🕸️ Spider-Man | **WEB** | For 6s, hitting a wall doesn't kill you — you web it and slingshot 90°. Other snakes still kill you. |
| 👊 Hulk | **SMASH** | Instantly eats **every fruit within 4 squares**, points, growth, power-ups and all. |
| 🐜 Ant-Man | **SHRINK** | For 5s you shrink and phase through other snakes, both ways. Walls and your own body still kill you. |
| 💻 Hacker | **HACK** | Steals a random 10–30 points. |

🦸 **Superman has no ability yet** — still purely cosmetic. Classic doesn't either.

**Everything is host-authoritative.** A guest pressing the button only *asks*;
the host checks the skin, the cooldown and whether you're alive before allowing
it. Tested: 3000 spammed requests in three seconds land exactly one use, for
every ability.

### 📊 How balanced is it? (simulated, 300 rounds, 6 players)

The answer changes completely with skill level, which was the surprise:

| Skin | Win % vs **weak** players | Win % vs **skilled** players |
|---|---|---|
| 🕸️ Spider-Man | **53%** 🚨 | 11% |
| 🔨 Thor | 13% | **33%** 🚨 |
| 🐜 Ant-Man | 11% | 20% |
| 🔆 Iron Man | 7% | 15% |
| Classic | 10% | 12% |
| 👊 Hulk | 6% | 9% |

*(a fair share would be ~17% each)*

- **Spider-Man is a beginner's crutch.** 93% of deaths among weak players are
  wall crashes, and WEB removes those for 6 seconds out of every 15. Against
  players who don't hit walls anyway, it's the *weakest* ability.
- **Thor is the opposite** — useless against players who are already crashing,
  dominant once everyone survives long enough to cluster together.
- Kill abilities cause **7% of deaths among weak players, 29% among skilled
  ones**. So it doesn't become a pure fighting game, but it's a real factor.
- Hulk's SMASH is the weakest overall — it only scores points, and points only
  break ties.

**If you want to even it out**, the knobs are all near the top of the file:

- Thor too strong → shorten `duration` (3500), shrink `HAMMER_RADIUS`, or make
  the hammer kill only on an exact square instead of 3×3.
- Spider-Man too strong for beginners → cut WEB `duration` from 6000 to ~3000.
- Hulk too weak → raise `SMASH_RADIUS` from 4, or give him a second effect.
- Everything too chaotic → raise `ABILITY_COOLDOWN_MS` from 15000.

⚠️ These numbers come from **simulated** players, not real ones. Treat them as a
rough guide — the honest test is six actual humans.

---

## ⚠️ What still needs doing---

## ⚠️ What still needs doing

**Upload it, then play it with real people.** Everything above passed automated
tests, but no human has actually played the 6-player version. Things worth
watching for:

- Does 6 snakes on a 40×40 board feel crowded or fun?
- Do the trails look good, or do they clutter the board and hide the fruit?
- Are the particles smooth on an older iPad, or do they cause stutter?
- Is ⚡ too strong? Is ❄️ annoying to be on the receiving end of?
- Does online play stay smooth with 5 friends, or does it lag?
- Are the fruits easy to tell apart at small sizes on a phone?
- Do the abilities feel fun or frustrating? Especially Thor's hammer, which the
  simulation says is the strongest against good players.
- Does the ability button get in the way on a phone?

Any of those are easy to tune — they're just numbers in the file.

---

## 💡 Round 4 — if you still want more

1. **Sound effects** — crunch on eating, zap for lightning, thud on crashing,
   fanfare for a reward *(you picked this — next up)*
2. **Obstacles and maps** — walls and mazes, pick a map before you play:
   Open, Cross, Maze, Donut *(you picked this — next up)*
3. **High score list** that survives closing the tab
4. **"Add to Home Screen"** so it feels like a real iPhone/iPad app (no App
   Store, no $99 developer account — a small change to the file)
5. **Computer opponents (bots)** so 1-player isn't lonely, and so you can
   practise 6-player without rounding up five friends
6. **Team mode** — 3 versus 3
7. **A homepage listing several games**, once there's a second game
8. **Respawn mode** — instead of watching after you crash, come back small and
   play to a time limit. Good if people get bored waiting

---

## 📝 Notes for next time

- Live site: **https://koolkande-lang.github.io/KanDeGamers/**
- Repo: **github.com/koolkande-lang/KanDeGamers**
- One single file, `index.html` — HTML, CSS and JavaScript all together
- Online play uses **PeerJS** from a CDN. Devices talk directly to each other;
  there is no server of ours and nothing to pay for
- The **host** device runs the real game and sends the picture to everyone else.
  Guests only draw what they're told and send their steering back
- Difficulty: Easy 230ms · Medium 160ms · Hard 110ms · Insane 75ms per move
  (bigger number = slower)
- Canvas is always 720×720 internally; the *number of squares* changes with
  player count, and CSS shrinks the display size to fit the screen

**Two things in the code that look odd but are deliberate:**

- The tail's glide point is **appended** to the body path, not written over the
  last one. Overwriting made the final segment span two squares, which visibly
  cut the corner whenever the tail rounded a bend.
- Steering from guests is routed through `matchConns`, a **frozen** copy of the
  lobby taken when the match starts — not the live lobby. If someone quits
  mid-game, the live list shrinks and everyone below them would slide onto the
  wrong snake.
