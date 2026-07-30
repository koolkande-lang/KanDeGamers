# KanDe Bros — Roadmap

**Two games now.** Nothing is uploaded yet.

## 📁 The site is now three files

| File | What it is |
|---|---|
| `index.html` | **KanDe Bros hub** — the front page listing both games |
| `snake.html` | Snake & Candy (this used to be `index.html`) |
| `wuzzle.html` | Wuzzle, the word game |

⚠️ **Upload all three together.** Snake has *moved* — if you upload the new
`index.html` without `snake.html`, the hub's Play button will 404.

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

### 🎮 Console-style menus

The menu used to be one long panel with everything stacked on it — speed,
colour, name, mode, bots, rewards, play buttons. It's now **seven separate
screens**, the way a console game does it.

```
HOME  ─┬─ ▶ PLAY        game mode · bots · 1P / 2P
       ├─ 🌐 ONLINE      create or join a room ─→ LOBBY
       ├─ 🎨 CUSTOMISE   name · colour ─→ 🏆 PATH OF PREY
       └─ ⚙️ SETTINGS    speed · key list
```

- Home shows a **profile strip**: your name, total points, how many of the 12
  rewards you have, and your equipped skin.
- Every sub-screen has a **◀ BACK** button and slides in from the right.
- **Back uses a stack**, so Home → Customise → Path → Back lands you on
  Customise, not Home. Getting that wrong is the classic menu bug.
- Squarer panels, uppercase spaced lettering, and a left accent bar that lights
  up on hover.

> ⚠️ The opening screen is set by calling `showPanel('mainMenu')` in code, not
> by trusting the `hidden` classes in the markup. That call has to be the **last
> line of setup** — `SCREENS` is declared further up, so calling it any earlier
> hits the temporal dead zone and the whole game fails to start.

### ✕ Quitting

There's a **✕ Quit** button under the board in every mode (or press **Escape**).

- **Two taps.** The first turns it red and asks "Really quit?"; a second within
  three seconds actually leaves. After three seconds it goes back to normal.
  Stops a stray thumb ending a good game.
- **You keep every point you scored.** It banks toward your Path exactly as if
  you'd crashed, and the results screen shows what you earned — including any
  reward you just unlocked.
- **Host quits** → everyone is told "The host ended the game" and taken to the
  results. Nobody is left staring at a snake that has quietly stopped moving.
- **Guest quits** → the host and everyone else carry on; the leaver's snake
  stays on the board but stops steering.

> ⚠️ The armed state is tracked with a **boolean**, not just a timestamp. Using
> `if (quitArmedAt)` looked fine but a clock reading of exactly `0` is falsy, so
> the second tap silently re-armed instead of quitting.

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

> ⚠️ **The guest must ask unconditionally.** An early version had the guest
> check its own copy first and bail out if it thought it had no ability — so
> any drift in the guest's local picture produced a completely dead button with
> no feedback. The host re-checks everything anyway, so the guest has no
> business refusing. Don't reintroduce that check.

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

### 🤖 Bots and team modes

**Game mode** and **Computer players** pickers sit on the main menu.

| Mode | Snakes | How it works |
|---|---|---|
| Free for all | you + 0–5 bots | Last snake alive wins |
| 1 v 1 | 2 | Two teams of one |
| 2 v 2 | 4 | Two teams of two |
| 3 v 3 | 6 | Two teams of three |

- **Empty seats fill with bots automatically** in team modes. Play 3v3 on your
  own if you like — you get five bots.
- Humans are dealt out **alternately**, so two friends land on opposite teams
  rather than both on one side.
- **Team colour beats personal colour.** In team games the glow around your
  snake shows 🔴 Red or 🔵 Blue, because which side someone's on matters more
  than which colour they picked.
- **No friendly fire.** Thor's hammer skips teammates and Iron Man's laser
  passes straight through them to hit the enemy behind. You *can* still crash
  into a teammate's body — that's just part of the game.
- A team is out when all its snakes have crashed. If both teams fall on the same
  tick, the higher **team total** wins.
- Bots get **random skins**, so they use abilities too. They obey the same 15
  second cooldown as you — tested.

**Bot difficulty**

| Level | How it plays |
|---|---|
| 🙂 Easy | Wanders, makes a mistake about a third of the time, rarely uses abilities |
| 😐 Medium | Chases the nearest fruit, avoids danger, uses abilities sensibly |
| 😈 Hard | Also runs a flood-fill to check it isn't sealing itself into a pocket, and uses abilities aggressively |

### 📊 How hard are the bots really? (simulated 1v1, 150 rounds)

Modelling "you" as a beginner who misreacts half the time:

| Bot level | You win | Your score | Bot's score |
|---|---|---|---|
| 🙂 Easy | **51%** | 156 | 206 |
| 😐 Medium | **13%** | 190 | 354 |
| 😈 Hard | **8%** | 179 | 371 |

- **Easy is a genuinely fair match** for a beginner — near enough a coin flip.
- **Medium already wins 87% of the time**, and Hard is only a little above that.
  The big jump is easy→medium, not medium→hard.
- The bots aren't cheating to do it. They see exactly what you see and share
  your cooldowns; they're just consistent. The flood-fill is what stops Hard
  bots trapping themselves, which is how most snake bots die.

If Medium feels brutal, raise its `mistake` value (0.12) in `BOT_LEVELS` near
the top of the file — that one number is most of the difficulty.

---

# 🔤 WUZZLE

A Boggle-style word game. Trace words through a 4×4 grid of letters before the
clock runs out.

**Rules** (real Boggle)

- Drag through **touching** letters — sideways, up, down or diagonally
- No square twice in the same word · 3 letters minimum
- **Qu** is one square but counts as two letters
- **Points = letters − 2.** 3 letters = 1, 4 = 2, 5 = 3, 6 = 4, and so on.
  Every extra letter is worth one more point
- **If two players find the same word, nobody scores it.** That's the real rule,
  and it's what makes the game about finding words others won't

**Scoring**

`points = letters − 2`, so 3→1, 4→2, 5→3, 6→4, 7→5, 8→6…

Boggle's real ladder is 1/1/2/3/5/11, which jumps around and is hard to explain.
The linear rule is easier to hold in your head and always rewards a longer word.

Side effect worth knowing: **scores are about 40% higher** than before, because
4-letter words (the most common kind) went from 1 point to 2. That makes texture
packs unlock faster:

| | first pack | all seven |
|---|---|---|
| beginner (~5 pts/round) | round 3 | round 17 |
| decent (~15 pts/round) | round 2 | round 8 |
| strong (~30 pts/round) | round 2 | round 3 |

If a strong player getting everything in three rounds feels too quick, raise the
`unlockAt` numbers in `THEMES` — they're the only thing that would need changing.

**Board sizes** (Solo → Board size, or Settings for the default)

| Size | Squares | Words hiding on it | Feel |
|---|---|---|---|
| 3 × 3 | 9 | ~69 | Quick. Extra vowels in the dice, or a small board starves |
| 4 × 4 | 16 | ~187 | Classic Boggle |
| 5 × 5 | 25 | ~413 | Big Boggle — far more to find |

- Each size uses a **real dice set**: the standard 16 for 4×4, the Big Boggle 25
  for 5×5, and a 9-dice set picked from the 4×4 dice with the vowel share
  raised to 46%.
- **Duds are rejected.** A raw random roll produced a 3×3 board with a *single
  word* in testing. Boards are now re-rolled until they clear a minimum (25 / 70 / 150 words). Solving costs under 5ms, so it's free.
- Online, the **host's size applies to everyone**. Guests are only sent the
  letters and work the size out from how many there are, so the two can never
  disagree.
- Tiles and gaps resize per board, so 5×5 still fits without scrolling.

> ⚠️ **A crash this caused.** `rollPlayableBoard()` rolled a board at the new
> size but solved it against the *old* neighbour map — so choosing 5×5 while the
> game was on 4×4 crashed on Start. Fixed at the root, and `solve()` now works
> the grid out from the board it's handed rather than trusting the current size.

**Modes**

- **Solo** — 1, 1½ or 3 minutes, then it shows you every word you missed and
  what percentage of the board's points you got
- **Online** — up to 8 players on the **identical board**, racing the same
  clock. Live "words found" counts while you play, full scores at the end

**The dictionary — 64,783 words**

Two sources merged:

1. A classic English word list, trimmed to words with real-world usage
2. The **most common 60,000 words from modern sources** — web, subtitles, news

> ⚠️ **Why the second source exists.** The first version used only the classic
> list, which is built from a **1934 dictionary**. It rejected `YAY`. And `YUP`,
> `OOPS`, `DUH`, `MEH`, `YIKES`, `HMM`, `OKAY`, `NAH` — plus `EMAIL`, `ONLINE`,
> `WEBSITE`, `BLOG`, `APP`, `EMOJI`, `SELFIE`, `TACO` and `SUSHI`. None of them
> existed in 1934. Lowering the frequency cutoff would not have helped: the
> words simply weren't in the book. It needed a modern source, not a looser
> filter.

**Keeping it clean.** Rude words are blocked by **generating inflections from
stems** rather than listing spellings by hand. The hand-written list missed
`SHITE` (stem + "e") and `CRAPPY` (doubled consonant) — English doubles the final
consonant before a vowel suffix, so the generator does too. 2,088 forms blocked
from 56 stems.

Matching is **exact-word, never substring**, so CLASS, GRASS, ASSIST, TITLE,
COCKPIT, PEACH and PUPPY are all untouched — verified by test.

Ordinary words like KILL, DEAD, BLOOD and GUN are left in. They're normal
English and appear in any book.

**Things worth knowing**

- Boards use the **real 16 Boggle dice**, not random letters. Random letters
  give unplayable consonant soup; these average ~86 findable words per board,
  and the worst of 50 test boards still had 23.
- The **host re-checks every word** a guest claims — that it's real, and that it
  can actually be traced on that board. A guest can send anything.
- During play only *counts* go over the wire, never the words themselves —
  otherwise you could read your opponents' answers off the network.

---

## 🐞 Bug sweep

A pass over both games looking for anything broken. Four real bugs found, all in
Wuzzle — Snake came through clean.

| Bug | What went wrong |
|---|---|
| **Quitting wiped your points** | Wuzzle threw away everything you'd scored when you left mid-round. Snake had always banked it. Now both do. |
| **Stale word counter** | `updateScore()` rebuilt a `<span id="foundCount">` that already existed in the markup — so the page had **two elements with the same id** and the original sat on "0 words" forever. |
| **"New pack!" banner shown twice** | A guest's results screen redraws (once waiting, once when the host's tally lands), and the unlock banner reappeared each time. |
| **Host tallied too early** | The host added up the instant its own clock hit zero. Guests' clocks start when the "start" message lands, so a word sent in the final moment could miss the count. The host now waits 700ms. |

Also clarified confusing wording: the results screen said "+3 to your total"
next to a table showing 2. Those are different numbers on purpose — pack
progress counts **your own words**, the match score applies the duplicate
cancellation — so it now reads "+3 towards texture packs".

**Two new test suites came out of this:**

- `wzonline.js` — boots **two (and three) complete copies of Wuzzle** wired by a
  fake network, and plays a real match: same board for everyone, words traced by
  dragging, duplicates cancelling, cheat attempts rejected, host leaving. This
  path had never been tested end to end.
- `structuretest.js` — checks all three pages for duplicate ids, unbalanced CSS,
  elements the code reaches for that don't exist, broken links, and ids created
  in JavaScript that clash with the markup. That last check is what would have
  caught the `foundCount` bug on day one.

> ⚠️ Both scanners produced **false alarms** first time by reading ids out of
> comments, CSS selectors and template strings. They now strip `<script>`,
> `<style>` and comments before looking. A test that cries wolf is worse than no
> test.

---

## ⚠️ What still needs doing### 🤖 Bots and team modes

**Game mode** and **Computer players** pickers sit on the main menu.

| Mode | Snakes | How it works |
|---|---|---|
| Free for all | you + 0–5 bots | Last snake alive wins |
| 1 v 1 | 2 | Two teams of one |
| 2 v 2 | 4 | Two teams of two |
| 3 v 3 | 6 | Two teams of three |

- **Empty seats fill with bots automatically** in team modes. Play 3v3 on your
  own if you like — you get five bots.
- Humans are dealt out **alternately**, so two friends land on opposite teams
  rather than both on one side.
- **Team colour beats personal colour.** In team games the glow around your
  snake shows 🔴 Red or 🔵 Blue, because which side someone's on matters more
  than which colour they picked.
- **No friendly fire.** Thor's hammer skips teammates and Iron Man's laser
  passes straight through them to hit the enemy behind. You *can* still crash
  into a teammate's body — that's just part of the game.
- A team is out when all its snakes have crashed. If both teams fall on the same
  tick, the higher **team total** wins.
- Bots get **random skins**, so they use abilities too. They obey the same 15
  second cooldown as you — tested.

**Bot difficulty**

| Level | How it plays |
|---|---|
| 🙂 Easy | Wanders, makes a mistake about a third of the time, rarely uses abilities |
| 😐 Medium | Chases the nearest fruit, avoids danger, uses abilities sensibly |
| 😈 Hard | Also runs a flood-fill to check it isn't sealing itself into a pocket, and uses abilities aggressively |

### 📊 How hard are the bots really? (simulated 1v1, 150 rounds)

Modelling "you" as a beginner who misreacts half the time:

| Bot level | You win | Your score | Bot's score |
|---|---|---|---|
| 🙂 Easy | **51%** | 156 | 206 |
| 😐 Medium | **13%** | 190 | 354 |
| 😈 Hard | **8%** | 179 | 371 |

- **Easy is a genuinely fair match** for a beginner — near enough a coin flip.
- **Medium already wins 87% of the time**, and Hard is only a little above that.
  The big jump is easy→medium, not medium→hard.
- The bots aren't cheating to do it. They see exactly what you see and share
  your cooldowns; they're just consistent. The flood-fill is what stops Hard
  bots trapping themselves, which is how most snake bots die.

If Medium feels brutal, raise its `mistake` value (0.12) in `BOT_LEVELS` near
the top of the file — that one number is most of the difficulty.

---

# 🔤 WUZZLE

A Boggle-style word game. Trace words through a 4×4 grid of letters before the
clock runs out.

**Rules** (real Boggle)

- Drag through **touching** letters — sideways, up, down or diagonally
- No square twice in the same word · 3 letters minimum
- **Qu** is one square but counts as two letters
- **Points = letters − 2.** 3 letters = 1, 4 = 2, 5 = 3, 6 = 4, and so on.
  Every extra letter is worth one more point
- **If two players find the same word, nobody scores it.** That's the real rule,
  and it's what makes the game about finding words others won't

**Scoring**

`points = letters − 2`, so 3→1, 4→2, 5→3, 6→4, 7→5, 8→6…

Boggle's real ladder is 1/1/2/3/5/11, which jumps around and is hard to explain.
The linear rule is easier to hold in your head and always rewards a longer word.

Side effect worth knowing: **scores are about 40% higher** than before, because
4-letter words (the most common kind) went from 1 point to 2. That makes texture
packs unlock faster:

| | first pack | all seven |
|---|---|---|
| beginner (~5 pts/round) | round 3 | round 17 |
| decent (~15 pts/round) | round 2 | round 8 |
| strong (~30 pts/round) | round 2 | round 3 |

If a strong player getting everything in three rounds feels too quick, raise the
`unlockAt` numbers in `THEMES` — they're the only thing that would need changing.

**Board sizes** (Solo → Board size, or Settings for the default)

| Size | Squares | Words hiding on it | Feel |
|---|---|---|---|
| 3 × 3 | 9 | ~69 | Quick. Extra vowels in the dice, or a small board starves |
| 4 × 4 | 16 | ~187 | Classic Boggle |
| 5 × 5 | 25 | ~413 | Big Boggle — far more to find |

- Each size uses a **real dice set**: the standard 16 for 4×4, the Big Boggle 25
  for 5×5, and a 9-dice set picked from the 4×4 dice with the vowel share
  raised to 46%.
- **Duds are rejected.** A raw random roll produced a 3×3 board with a *single
  word* in testing. Boards are now re-rolled until they clear a minimum (25 / 70 / 150 words). Solving costs under 5ms, so it's free.
- Online, the **host's size applies to everyone**. Guests are only sent the
  letters and work the size out from how many there are, so the two can never
  disagree.
- Tiles and gaps resize per board, so 5×5 still fits without scrolling.

> ⚠️ **A crash this caused.** `rollPlayableBoard()` rolled a board at the new
> size but solved it against the *old* neighbour map — so choosing 5×5 while the
> game was on 4×4 crashed on Start. Fixed at the root, and `solve()` now works
> the grid out from the board it's handed rather than trusting the current size.

**Modes**

- **Solo** — 1, 1½ or 3 minutes, then it shows you every word you missed and
  what percentage of the board's points you got
- **Online** — up to 8 players on the **identical board**, racing the same
  clock. Live "words found" counts while you play, full scores at the end

**The dictionary**

- Stored **front-coded**: an uppercase letter says how many characters this word
  shares with the previous one, then the rest. 306 KB → 135 KB, and 69 KB
  gzipped over the wire

**🎨 Texture packs** (Settings → Texture pack)

Six looks for the board. Cosmetic only — same words, same scores, same rules.

| Pack | Look |
|---|---|
| 🌊 Ocean | The original deep blue. Default. |
| ☀️ Sunny | Warm daylight — cream tiles on amber, dark brown letters |
| 🍃 Windy | Pale and airy — white/mint tiles, teal letters |
| ⛈️ Stormy | Dark and moody — near-black tiles, glowing violet letters |
| ❄️ Frosty | Icy — white-blue tiles, deep blue letters |
| 🪵 Sturdy | Stone and wood — brown tiles, mossy green selection |

- A pack is just **11 CSS variables**. Adding one means adding a row of colours
  to the `THEMES` list — no new CSS, no new markup.
- Your choice is saved on the device and the board **fades** between packs
  rather than snapping.
- **Every pack is contrast-checked in the tests.** The first attempt looked fine
  on the unselected tiles but five of six packs had barely-readable letters
  *while selected* — which is exactly when you're staring at them mid-drag. The
  test now requires 4.5:1 (the standard for normal text) for both the resting
  and the selected state, and every pack clears it.

**Fitting on one screen**

Nothing in Wuzzle or the hub ever scrolls. Two things make that true:

1. **Everything is sized in `vh`/`clamp()`** — text, padding, the board and the
   word list all shrink on a short screen before anything else happens.
2. **A measured fit-to-screen scale as a safety net.** After layout, the page
   measures its own content and applies a CSS `scale()` if it still doesn't fit.
   It never scales *up* (that would blur things), only down.

`html,body{overflow:hidden}` means a mistake shows up as clipped content rather
than a silent scrollbar — much easier to notice and fix.

> ⚠️ On a **phone held sideways** there's very little height, so the scale can
> get small. If that reads badly, the fix is a two-column landscape layout
> rather than loosening the no-scroll rule.

**Who's playing, and who's winning**

- In the lobby and during the game, everyone sees **the list of players' names**
  — so you know who you're up against.
- **Nobody sees anyone else's score or word count until the round ends.** The
  host doesn't get a peek either. An earlier version broadcast live counts;
  that's now removed and `pushLive()` is a deliberate no-op with a comment
  saying why.

**⚠️ The one that got away — tracing stopped working**

While restyling, the letter squares were renamed from `.tile` to `.tileL` (to
stop them clashing with the home-screen menu tiles). The place that *creates*
them was updated; the place that *hit-tests* them was not. `tileAt()` went on
looking for `.tile`, never matched anything, and **dragging silently did
nothing at all**.

Two things stop it happening again:

- The class name now lives in a single `TILE_CLASS` constant, declared at the
  top of the file, used by both the renderer and the hit-test.
- `dragtest.js` drives the **real pointer handlers** with real coordinates —
  pointerdown, a series of pointermoves across squares, pointerup — and asserts
  the word is accepted. Verified by putting the bug back: the test fails.

The deeper cause was a **gap in the test harness**, not the game. The fake DOM
never connected `.className` to `.classList`, so a class-name mismatch was
invisible to every test. It does now.

**Things worth knowing**

- Boards use the **real 16 Boggle dice**, not random letters. Random letters
  give unplayable consonant soup; these average ~86 findable words per board,
  and the worst of 50 test boards still had 23.
- The **host re-checks every word** a guest claims — that it's real, and that it
  can actually be traced on that board. A guest can send anything.
- During play only *counts* go over the wire, never the words themselves —
  otherwise you could read your opponents' answers off the network.

---

## 🐞 Bug sweep

A pass over both games looking for anything broken. Four real bugs found, all in
Wuzzle — Snake came through clean.

| Bug | What went wrong |
|---|---|
| **Quitting wiped your points** | Wuzzle threw away everything you'd scored when you left mid-round. Snake had always banked it. Now both do. |
| **Stale word counter** | `updateScore()` rebuilt a `<span id="foundCount">` that already existed in the markup — so the page had **two elements with the same id** and the original sat on "0 words" forever. |
| **"New pack!" banner shown twice** | A guest's results screen redraws (once waiting, once when the host's tally lands), and the unlock banner reappeared each time. |
| **Host tallied too early** | The host added up the instant its own clock hit zero. Guests' clocks start when the "start" message lands, so a word sent in the final moment could miss the count. The host now waits 700ms. |

Also clarified confusing wording: the results screen said "+3 to your total"
next to a table showing 2. Those are different numbers on purpose — pack
progress counts **your own words**, the match score applies the duplicate
cancellation — so it now reads "+3 towards texture packs".

**Two new test suites came out of this:**

- `wzonline.js` — boots **two (and three) complete copies of Wuzzle** wired by a
  fake network, and plays a real match: same board for everyone, words traced by
  dragging, duplicates cancelling, cheat attempts rejected, host leaving. This
  path had never been tested end to end.
- `structuretest.js` — checks all three pages for duplicate ids, unbalanced CSS,
  elements the code reaches for that don't exist, broken links, and ids created
  in JavaScript that clash with the markup. That last check is what would have
  caught the `foundCount` bug on day one.

> ⚠️ Both scanners produced **false alarms** first time by reading ids out of
> comments, CSS selectors and template strings. They now strip `<script>`,
> `<style>` and comments before looking. A test that cries wolf is worse than no
> test.

---

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
- Do the new menu screens feel better, or is it now too many taps to start a
  game? (Home → Play → 1 Player is 3 taps, where it used to be 1.)

**Wuzzle specifically:**

- Is tracing accurate on a phone, or do fingers slip between squares?
- Is 1½ minutes the right default round?
- Does the dictionary reject words kids think are real? That's the most likely
  complaint. The fix is to lower the frequency cutoff from 2.0 and rebuild.
- Are 8 players too many for one board?
- On a phone in landscape, does the fit-to-screen scale get too small to read?
- Are Easy bots actually beatable for a real beginner, and is Medium too big a
  jump? The simulation says easy→medium is a cliff.
- In team modes, is it obvious at a glance who's on your side?

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
5. **A homepage listing several games**, once there's a second game
6. **Respawn mode** — instead of watching after you crash, come back small and
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

**Bugs found by running two real copies of the game against each other**
(`onlinetest.js` boots a host and a guest in isolated VM contexts and wires
their fake PeerJS together — the only way to test the online path properly):

1. **Guests couldn't use abilities.** `requestAbility()` checked the guest's own
   copy of itself and returned early if it looked wrong — silently. Now the
   guest always asks and the host decides.
2. **Bots were different colours on every screen.** The host broadcast the
   roster *before* assigning colours, and bots join with no colour, so guests
   drew them all green while the host drew them properly.
3. **A connection with no lobby seat was told it was "player -1"**, which
   permanently broke that player's controls. Now skipped, and guests ignore a
   nonsense index.

**Three things in the code that look odd but are deliberate:**

- The tail's glide point is **appended** to the body path, not written over the
  last one. Overwriting made the final segment span two squares, which visibly
  cut the corner whenever the tail rounded a bend.
- Steering from guests is routed through `matchConns`, a **frozen** copy of the
  lobby taken when the match starts — not the live lobby. If someone quits
  mid-game, the live list shrinks and everyone below them would slide onto the
  wrong snake.
- The guest shows a brief **⏳** on the ability button after pressing. The real
  answer comes back from the host within ~45ms, but without that placeholder a
  laggy press looks like the button is broken — which is exactly how this bug
  got reported in the first place.
