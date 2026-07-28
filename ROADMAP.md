# Snake & Candy — Ideas List

Everything we want to add, written down so nothing gets forgotten.

**Nothing here is built yet.** This is the wish list.

> 📌 **Upload this file to your GitHub repo** (same place as `index.html`).
> Then it lives with the project forever, and next time we work together I can
> read it straight from the repo and pick up exactly where we left off.

---

## ✅ Already done

- Snake eats candy, score goes up
- 1 player
- 2 player on the same device
- 2 player online with a room code
- On-screen arrow buttons
- **Swipe to steer** (new)
- **Four speed levels: Easy / Medium / Hard / Insane** (new)

⚠️ The two "new" ones are finished but **not uploaded to the website yet.**

---

## 🎯 The top three (your picks)

### 1. Move the arrow buttons to the right of the board
**Why:** On an iPad the buttons sit below the board, so you have to scroll down to reach them. Annoying mid-game.

**Plan:** On wide screens, put the board on the left and the arrows on the right, side by side. On narrow phones, keep them below where they are now. Everything fits on one screen, no scrolling.

**Difficulty:** 🟢 Easy — this is a layout change only, no game logic touched.

---

### 2. Make the snake look more realistic
**Why:** Right now it's a line of plain squares. It should look like an actual snake.

**Ideas for what "realistic" could mean — pick your favourites:**

- Rounded body instead of squares
- Segments joined together so it's one smooth ribbon, not a dotted line
- **Eyes on the head**, looking in the direction it's moving 👀
- A flicking tongue
- A tail that tapers to a point
- Smooth corners when it turns
- Body that glides between squares instead of jumping (this one is the hardest, but it's what makes it feel *alive*)

**Difficulty:** 🟡 Medium — it's all drawing code, so it can't break the gameplay. Safe to experiment with.

---

### 3. More players — 3 or 4 at once
**Why:** So the whole group can play together instead of just two.

**The honest catch:** this is the big one. Right now the code is built around exactly two snakes — there's a `snake1` and a `snake2`, written out by hand. To support four, that has to become a *list* of snakes that can be any length. It's not hard, it's just a lot of pieces to change at once.

The online part also changes: today the host talks to **one** friend. It would need to talk to **all** friends at the same time and keep everyone's screens in sync.

**Difficulty:** 🔴 Hard — the biggest job on this list. Worth it though.

**Questions to answer before we start:**

- Max players — 4? 6?
- Everyone online, or also 3–4 people crowded around one iPad?
- What happens when one snake dies — do they watch, or respawn?
- Does the room code screen need a "waiting for players" lobby?

---

## 💡 The other ideas

### 4. Bigger map
**Why:** More room to move, and it's needed anyway if 4 snakes are sharing the board.

The board is 24×24 squares today. Could go to 32×32 or bigger.

**Difficulty:** 🟢 Easy, with one thing to watch: more squares on the same screen = smaller squares. On a phone they could get too tiny to see. Might need the map size to depend on how many players there are.

---

### 5. More fruits on the map at once
**Why:** Only one candy exists at a time, so everyone races for the same one. Boring, and unfair to whoever's further away.

**Plan:** Have 3–5 fruits out at once.

**Fun extra:** different fruits could do different things —

| Fruit | Effect |
|---|---|
| 🍬 Candy | +10 points (normal) |
| 🍒 Cherry | +25 points, rarer |
| 🍌 Banana | Makes you shorter — an escape hatch when you're huge |
| ⚡ Lightning | Speed burst for a few seconds |
| ❄️ Ice | Slows *everyone else* down |

**Difficulty:** 🟢 Easy for plain extra fruits. 🟡 Medium for the special powers.

---

### 6. Pick your own snake colour
**Why:** So each player can be their own colour instead of always green and blue.

**Plan:** Colour swatches on the menu screen. Your pick gets sent to the other players so everyone sees the same thing. Needs a rule to stop two people picking the same colour.

**Difficulty:** 🟡 Medium — easy to draw, slightly fiddly to sync over the internet.

---

## 🔨 Suggested build order

Here's the thing worth knowing: **#5 (more fruits) and #6 (colours) both touch the same code as #3 (more players).**

If we build them before the multiplayer rewrite, we'd have to build them a second time afterwards. So it's smarter to group them.

**Round 1 — quick wins, low risk**

1. Arrow buttons to the right (#1)
2. Realistic snake (#2)
3. Bigger map (#4)

Nothing here can break the game. Ship it fast, see it live.

**Round 2 — the foundation**

4. Rewrite for any number of players (#3)

This is the heavy one. Doing it here means colours and fruits become easy afterwards instead of being done twice.

**Round 3 — riding on the foundation**

5. Multiple fruits (#5)
6. Player colours (#6)

**Round 4 — if you still want more**

7. Special power-up fruits
8. High score list
9. Sound effects
10. "Add to Home Screen" so it feels like a real iPhone/iPad app

---

## 📝 Notes for next time

- Live site: **https://koolkande-lang.github.io/KanDeGamers/**
- Repo: **github.com/koolkande-lang/KanDeGamers**
- The game is one single file, `index.html` — HTML, CSS and JavaScript all together
- Online play uses **PeerJS**, loaded from a CDN. Phones talk directly to each other; there's no server of ours
- The **host** device runs the actual game and sends the picture to everyone else. Guests only draw what they're told
- Difficulty speeds: Easy 230ms · Medium 160ms · Hard 110ms · Insane 75ms (bigger number = slower)
- Board is 24×24 squares on a 480×480 canvas
