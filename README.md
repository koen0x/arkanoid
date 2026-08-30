# 🧱 Arkanoid

A browser-based recreation of **Taito's classic 1986 Arkanoid**.

One HTML file. No installation. No framework. No server. Just open it and play. 👾

## 🎮 Play online

**[Play Arkanoid](https://koen0x.github.io/arkanoid/arkanoid.html)**

## ✨ Features

- 🧱 32 regular Arkanoid rounds
- 👹 Round 33 with **DOH**
- 💊 Classic power-ups:
  - **L** Laser
  - **E** Expand
  - **C** Catch
  - **S** Slow
  - **B** Break
  - **D** Disruption
  - **P** Extra Life
- 👾 Enemies and top-door spawning
- 🔊 Embedded game audio
- 🏆 Persistent high score
- 🎨 Classic rotating playfield backgrounds
- 🤖 Optional autoplay
- 🕹️ Attract/demo mode
- 🖥️ Browser fullscreen
- ⏱️ Fixed 60 Hz game simulation

Everything required to play is contained inside:

```text
arkanoid.html
```

No external assets or network connection are required after loading the file.

## 🕹️ Controls

| Key / input | Action |
|---|---|
| **← / →** | Move the Vaus |
| **Mouse / pointer** | Move the Vaus |
| **Space** | Release ball / fire Laser |
| **Click** | Release ball / fire Laser |
| **M** | Toggle sound |
| **F** | Toggle fullscreen |
| **A** | Toggle autoplay |

### Round selection

On the title screen, type a round number from **1 to 33** and press **Enter**.

Press **Space** to start normally from Round 1.

## 🤖 Autoplay

Press **A** during the game to let the computer take control of the Vaus.

Autoplay uses the same paddle movement and game actions as a normal player. It can catch capsules, fire the Laser, release caught balls and use the Break exit.

Because sometimes it's fun to watch the machine fight the machine. 🤖⚔️👾

## 👹 Round 33

Round 33 contains the final **DOH** encounter and is handled separately from the normal brick rounds.

You can jump directly to it from the title screen:

```text
33 + Enter
```

Good luck. 😈

## 💾 High score

Your high score is stored locally in the browser using:

```text
localStorage["arkanoid.highScore"]
```

It stays on your device between sessions unless browser storage is cleared.

## 📦 Standalone version

The entire playable game lives in a single self-contained HTML file.

That makes it easy to:

- play locally
- host on GitHub Pages
- copy to another computer
- keep an offline version

No build step is required for the public release.

## ❤️ About this project

This is an independent, non-commercial browser reconstruction inspired by the original **Arkanoid**, created by **Taito Corporation** in 1986.

The project is not affiliated with, sponsored by, or endorsed by Taito.

Arkanoid and related names, characters and original game assets remain the property of their respective rights holders.

---

🧱 **Break bricks. Catch capsules. Defeat DOH.**

**[▶ Play now](https://koen0x.github.io/arkanoid/arkanoid.html)**
