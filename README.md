# Neural Canvas

**Paint glowing light in mid-air — with your bare hands.** *Hack the Arts 2026 submission.*

Neural Canvas turns your webcam into a paintbrush. A neural network watches your hands
in real time and turns your motion into living, glowing art. There is **no brush, no
mouse, no touchscreen** — you pinch your fingers together in the air and light follows
your fingertip. **This is art that cannot exist without the technology that perceives it.**

It runs **entirely in your browser** — the camera feed never leaves your device.

▶ **Live:** https://danny-397.github.io/neural-canvas/

---

## How to use it

1. Open the site and press **Start camera** (allow camera access).
2. **🤏 Pinch** your thumb and index finger together — light paints from your fingertip.
3. Move your hand to draw. Unpinch to lift the "pen." Works with **both hands at once.**

### Hand gestures

| Gesture | Action |
|---|---|
| 🤏 Pinch | Paint |
| ✋ Open palm | Erase |
| ✌️ Victory | Next color |
| 👎 Thumb down | Undo |
| 👍 Thumb up | Clean view (hide the UI to admire / screenshot) |
| ✊ Fist (hold) | Clear the canvas |

## Features

- **Live hand tracking** — Google's MediaPipe locates 21 3D points on each hand ~60× a
  second, fully on-device.
- **Brushes** — Neon glow, Ribbon, Spray, Comet, and live **Embers** that drift and fade.
- **Kaleidoscope symmetry** — mirror or 4/6/8-fold folding turns a single stroke into a
  living mandala.
- **Full-body mode** — swaps in a pose model so you can paint with your whole body.
- **Two-hand colors, rainbow, adjustable size, backdrops, and bloom.**
- **Attract mode** — left idle, the canvas paints its own drifting mandala to draw a crowd,
  then hands control back the moment someone raises a hand.
- **Audio-reactive glow, undo, fullscreen, Save PNG, and Record WebM.**

## How it works

Every webcam frame is passed to a pre-trained **MediaPipe** gesture/hand model
([tasks-vision](https://developers.google.com/mediapipe)), which returns the 3D position of
each hand joint and a classified gesture. The app reads those points — your index fingertip
is the brush, a pinch is the pen — and a **one-euro filter** smooths the tracking so lines
stay clean. Symmetry mirrors every stroke into a live kaleidoscope. The machine doesn't make
the art; **you** do. But you couldn't paint in mid-air unless a neural network perceived
your motion in real time.

## Tech

Pure HTML/CSS/JS in a single file, no build step and no server. MediaPipe Tasks Vision
(WebAssembly + GPU) loaded from a CDN; rendering via the Canvas 2D API.

```
index.html   → the app
cppn.html    → an earlier experiment: an abstract generative-art tool (a CPPN/SIREN
               network that computes an image directly from pixel coordinates). Kept for
               reference; the hand-painting app above is the actual submission.
```

Created for **Hack the Arts 2026** — *art that wouldn't exist without technology.*
