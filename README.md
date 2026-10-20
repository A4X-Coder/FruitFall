<div align="center">

# 🍉 Fruitfall — Endless Merge

**A juicy, physics-based fruit merging puzzle that runs in a single HTML file.**
No build step. No dependencies. No install. Just open it and play.

### ▶️ [**Play now: a4x-coder.github.io/FruitFall**](https://a4x-coder.github.io/FruitFall/)

[![Play](https://img.shields.io/badge/play-live%20demo-f45198)](https://a4x-coder.github.io/FruitFall/)
![Single file](https://img.shields.io/badge/single%20file-index.html-8e7087)
![Dependencies](https://img.shields.io/badge/dependencies-none-ff9b38)
![Theme](https://img.shields.io/badge/theme-light%20%2B%20dark-452b43)

🍒 → 🍓 → 🍇 → 🍊 → 🍎 → 🍐 → 🍑 → 🍍 → 🥥 → 🍈 → 🍉

</div>

---

## 🎮 About

Drop fruits into the bowl. When two **identical** fruits touch, they merge into the next fruit in the chain. Chain merges quickly to build combos, climb all the way to the 🍉 Watermelon, and don't let the pile cross the limit line.

The whole game is one `index.html` file, built with plain HTML, CSS and JavaScript on a `<canvas>`, and it's hosted for free on GitHub Pages. It works on phones, tablets and desktops.

## ✨ Features

- **Custom physics:** a position-based Verlet engine running at a fixed 480 Hz, so it feels the same on every device and refresh rate.
- **Combo system:** merge again within 1.3 seconds to build a chain. Each link adds +0.5× to the score multiplier, and the merge sound climbs in pitch.
- **11 fruit levels:** from 🍒 Cherry (2 pts) up to 🍉 Watermelon (2048 pts), with a legend that lights up as you unlock each one.
- **Mega merge:** joining two 🍉 Watermelons clears them for a **3000-point** bonus.
- **Fair game over:** the bowl only counts as full when a fruit stays resting above the limit line for 2.5 seconds. Fruits that are still bouncing or flying don't count, and a warning countdown appears before it's over.
- **Aim guide:** a dotted line and ghost fruit show exactly where your drop will land.
- **Juice:** pop animations, particles, shockwave rings, floating score text, screen shake and optional vibration.
- **Light and dark theme:** follows your system setting on first launch, with a toggle button. Your choice is remembered.
- **Sound:** all effects are generated live with the Web Audio API (no audio files). One tap to mute.
- **Personal best:** saved in your browser, with a "NEW BEST!" celebration.
- **Pause and resume:** pauses automatically when you switch tabs or apps.
- **Responsive:** a fixed logical world scaled to any screen, sharp on high-DPI displays and safe-area aware on phones.

## 🕹️ How to play

| Action | Touch / Mouse | Keyboard |
| --- | --- | --- |
| Aim | Drag across the bowl | `←` / `→` |
| Drop fruit | Release your finger or click, or tap **DROP FRUIT** | `Space` or `↓` |
| Pause / resume | **Ⅱ** button | `P` |
| New game | **↻** button | `Space` on the start or game-over screen |

**Tips**

1. Keep big fruits in the corners and build the pile towards one side.
2. Plan your merges so they chain into each other for a big combo.
3. Watch the **NEXT** fruit in the top corner.
4. Keep the area under the limit line clear. You get a brief red warning before it's over.

## 🏆 Scoring

| Level | Fruit | Points |
| :-: | :-: | --: |
| 1 | 🍒 Cherry | 2 |
| 2 | 🍓 Strawberry | 4 |
| 3 | 🍇 Grape | 8 |
| 4 | 🍊 Orange | 16 |
| 5 | 🍎 Apple | 32 |
| 6 | 🍐 Pear | 64 |
| 7 | 🍑 Peach | 128 |
| 8 | 🍍 Pineapple | 256 |
| 9 | 🥥 Coconut | 512 |
| 10 | 🍈 Melon | 1024 |
| 11 | 🍉 Watermelon | 2048 |
| — | 🍉 + 🍉 | 3000 (mega) |

Points are awarded for the fruit you **create**. Combo multiplier: `1 + 0.5 × (chain − 1)`.
Only the first five fruits (🍒 to 🍎) are ever dropped; the rest have to be earned by merging.

## 🚀 Run it yourself

### Option 1: Play online

Open **[a4x-coder.github.io/FruitFall](https://a4x-coder.github.io/FruitFall/)** in any modern browser.

### Option 2: Open the file

Download `index.html` from this repository and open it in your browser. It works offline.

### Option 3: Local server

```bash
git clone https://github.com/A4X-Coder/FruitFall.git
cd FruitFall
python3 -m http.server 8000
# then visit http://localhost:8000
```

## 🛠️ Tweaking the game

Everything lives in `index.html`. The easiest knobs are near the top of the `<script>`:

| What | Where | Default |
| --- | --- | --- |
| Limit line height | `LINE` | `92` |
| Time above the line before game over | `DANGER_MAX` | `2.5` seconds |
| Fruit sizes, colors and points | the `F` array | 11 fruits |
| Which fruits can be dropped, and how often | `WEIGHTS` | cherry to apple, weighted toward small |
| Gravity | `g=1700*h*h` in `step()` | `1700` |
| Combo window | `comboT=1.3` in `doMerge()` | `1.3` seconds |
| Colors | CSS variables in `:root` and `[data-theme="dark"]` | pink and plum |

## 🧠 How it works

- **Fixed world, flexible screen.** The game logic always runs in a `360 × 460` coordinate space and is scaled to the canvas, so physics are identical on every device.
- **Verlet integration.** Each fruit stores its current and previous position, so velocity is implicit. Collisions are resolved by pushing overlapping fruits apart, weighted by mass.
- **Stability guards.** Speed is capped per step (upward most strictly) and push-out distance is limited, so deep overlaps or rapid drops can't launch a fruit out of the bowl.
- **Pre-rendered sprites.** Each fruit's body, emoji and highlight are drawn once per screen size onto small offscreen canvases, then reused every frame for smooth rendering.
- **Live audio.** Merge sounds are short oscillator tones whose pitch follows the fruit level and combo count.
- **Local storage.** Your best score, theme and sound setting are stored under `fruitfall-best`, `fruitfall-theme` and `fruitfall-sound`. If storage is blocked, the game still works.

## 🌐 Browser support

Works in current versions of Chrome, Edge, Firefox and Safari, on desktop and mobile. Emoji are rendered by your system's emoji font, so fruit artwork looks slightly different on Apple, Google, Windows and Samsung devices.

## 🤝 Feedback and ideas

Found a bug or have an idea? [Open an issue](https://github.com/A4X-Coder/FruitFall/issues). Some directions that would be fun:

- Leaderboards or daily challenges
- More fruit sets or themes
- Power-ups (shake the bowl, remove a fruit, bomb)
- Installable PWA with offline play
- Custom sound packs

## 📄 License

No license is specified in this repository unless a LICENSE file is added. Until then, reuse and redistribution permissions should not be assumed.

---

<div align="center">

Made with 🍓 and a little physics by [A4X-Coder](https://github.com/A4X-Coder)

</div>
