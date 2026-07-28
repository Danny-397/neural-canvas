# Neural Canvas — Devpost writeup & demo script

*Hack the Arts 2026 — theme: "create art that wouldn't exist without technology."*

▶ **Live:** https://danny-397.github.io/neural-canvas/ · **Repo:** https://github.com/Danny-397/neural-canvas

---

## Inspiration
We wanted art you make with your **whole body**, not a mouse. What if the paintbrush was
your bare hand, moving through empty air? That's only possible if a machine can *perceive*
you — so the technology isn't a filter bolted on top of the art, it's the only reason the
art can exist at all. That's the purest read of the theme: paint in mid-air, and let a
neural network be the thing that sees your hand.

## What it does
Neural Canvas turns your webcam into a paintbrush.

- **Pinch to paint.** A neural network tracks 21 points on each hand in real time; pinch
  your thumb and index finger and glowing light follows your fingertip through the air.
- **Gestures, not menus.** ✋ open palm erases, ✌️ changes color, 👎 undoes, ✊ clears,
  👍 hides the UI for a clean view. Both hands work at once.
- **Kaleidoscope symmetry.** Mirror or 4/6/8-fold folding turns one gesture into a living
  mandala.
- **Brushes** — neon glow, ribbon, comet, spray, and live embers that drift up and fade.
- **Full-body mode** — a pose model lets you paint with your whole body, not just hands.
- **Attract mode** — left alone, the canvas paints its own drifting mandala to pull a
  crowd, then instantly hands control back when someone raises a hand.
- Plus rainbow/two-hand colors, backdrops, bloom, undo, fullscreen, **Save PNG**, and
  **Record WebM**.

## How we built it
A single HTML file — no build step, no server, no data leaving the device. Each webcam
frame is fed to Google's **MediaPipe Tasks Vision** gesture/hand model (WebAssembly + GPU,
loaded from a CDN), which returns 3D hand-joint positions and a classified gesture ~60× a
second. We read the index fingertip as the brush and a pinch as the pen, smooth the raw
tracking with a **one-euro filter** to kill jitter, and render glowing strokes with the
Canvas 2D API (additive blending + shadow-blur glow). Symmetry is a set of coordinate
transforms applied to every stroke; the ember brush drives a small particle system on its
own layer.

## Challenges we ran into
Raw hand-tracking is jittery — a fingertip position wobbles several pixels per frame, which
makes ugly, shaky lines. The fix was a **one-euro filter**, which adapts its smoothing to
how fast you're moving: heavy smoothing when your hand is still (clean lines), light
smoothing when you move fast (no lag). Tuning the **pinch threshold** was the other hard
part — it has to work whether your hand is near or far from the camera, so we measure the
pinch distance *relative to the size of your hand* rather than in absolute pixels.

## Accomplishments we're proud of
- It feels like magic the first time light follows your finger through the air.
- Everything is gesture-driven — you never touch the keyboard once the camera is on.
- It's a genuine crowd-pleaser: attract mode + kaleidoscope makes a great live booth.
- 100% on-device and private; nothing is uploaded.

## What we learned
How real-time pose/hand estimation works in the browser, why raw landmark data needs
adaptive filtering, and how to design an interaction that's legible to a first-time user
with zero instructions (gesture key + on-screen cursor + status hints).

## What's next
Multiplayer (two people painting the same canvas over the network), foot/leg tracking for
full-body dance painting, and a gallery of recorded pieces.

---

## 🎤 60-second demo script
1. **(0:00) Hook.** Walk up while **attract mode** is painting itself. "This whole thing is
   painted with your hands — watch." Raise your hand; the demo hands you control.
2. **(0:10) Paint.** Pinch and draw a glowing line in the air. "There's no mouse and no
   touchscreen. A neural network is tracking my hand 60 times a second — the light just
   follows my finger."
3. **(0:22) Gestures.** ✌️ change color, ✋ erase, 👎 undo. "Every control is a gesture —
   I never touch the keyboard."
4. **(0:36) Payoff.** Turn on **6-fold symmetry** and sweep both hands. "One motion becomes
   a living mandala." Add **bloom** / **embers** for the wow moment.
5. **(0:50) Theme.** 👍 for a clean view of the finished piece. "This art literally cannot
   exist without the technology — because the technology is the only thing that can *see*
   me paint."

## ✅ Pre-demo test checklist (run on your actual demo laptop + good lighting)
- [ ] Page loads over **https**; camera permission granted; landing overlay dismisses.
- [ ] Pinch paints; unpinch lifts; both hands work.
- [ ] Gestures: ✋ erase, ✌️ color, 👎 undo, 👍 view, ✊ hold-to-clear.
- [ ] Brushes (neon/ribbon/spray/comet/embers) and size slider all visibly change strokes.
- [ ] Symmetry 4/6/8-fold + mirror; bloom; backdrops.
- [ ] Body mode: raise a hand above your shoulder to paint.
- [ ] Attract mode kicks in after ~15s idle and releases when you raise a hand.
- [ ] Save PNG downloads; Record produces a WebM.
- [ ] Fullscreen for presenting.

## ✨ Framing lines (for the pitch / booth sign)
- "No brush. No mouse. No touchscreen. Just your hands and light."
- "The technology isn't on top of the art — it's the only reason the art can exist. It's
  the thing that can *see* you paint."
