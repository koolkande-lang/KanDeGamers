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

---

## ⚠️ What still needs doing

**Upload it, then play it with real people.** Everything above passed automated
tests, but no human has actually played the 6-player version. Things worth
watching for:

- Does 6 snakes on a 40×40 board feel crowded or fun?
- Is ⚡ too strong? Is ❄️ annoying to be on the receiving end of?
- Does online play stay smooth with 5 friends, or does it lag?
- Are the fruits easy to tell apart at small sizes on a phone?

Any of those are easy to tune — they're just numbers in the file.

---

## 💡 Round 4 — if you still want more

1. **High score list** that survives closing the tab
2. **Sound effects** — crunch on eating, thud on crashing
3. **"Add to Home Screen"** so it feels like a real iPhone/iPad app (no App
   Store, no $99 developer account — a small change to the file)
4. **Team mode** — 3 versus 3
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

**Two things in the code that look odd but are deliberate:**

- The tail's glide point is **appended** to the body path, not written over the
  last one. Overwriting made the final segment span two squares, which visibly
  cut the corner whenever the tail rounded a bend.
- Steering from guests is routed through `matchConns`, a **frozen** copy of the
  lobby taken when the match starts — not the live lobby. If someone quits
  mid-game, the live list shrinks and everyone below them would slide onto the
  wrong snake.
