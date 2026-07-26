# Neural Canvas — Devpost writeup & demo script

*Hack the Arts 2026 — theme: "create art that wouldn't exist without technology."*

▶ **Live:** https://danny-397.github.io/neural-canvas/ · **Repo:** https://github.com/Danny-397/neural-canvas

---

## Inspiration
Most "AI art" is really a photo of a dataset — pixels sampled from millions of existing
images. We wanted the opposite: art with **no pixels and no dataset at all**, where the
artwork *is* the neural network. A Compositional Pattern Producing Network (CPPN) computes
a color for every coordinate on demand, so the picture literally does not exist until the
network imagines it. That's the purest possible answer to "art that wouldn't exist without
technology."

## What it does
Neural Canvas turns a small neural network into an interactive canvas you **evolve**:

- **Every image is a network.** A CPPN maps `(x, y, radius, α, β, γ) → (R, G, B)`.
- **🧬 Breed** — pick two artworks; get a *generation grid* of nine offspring (weight
  crossover). Click one to breed a new generation from it, again and again — interactive
  neuro-evolution in the lineage of Picbreeder/NEAT. Your taste is the fitness function.
- **🌀 Morph** — smoothly interpolate the network's weights between two artworks; a
  hypnotic transition you can record.
- **⚛ Mutate** — perturb the weights to explore nearby variations.
- **✦ Name Art** — type any word; it's hashed into a seed, so your name always makes the
  same piece. Language → picture.
- **♾ Infinite zoom** — the image is a *function*, not pixels, so you can zoom forever and
  **Export HD** at any resolution.
- **🔷 Symmetry**, **🎙 Audio React** (mic drives the latent vector), **⏺ Record** (WebM),
  and **🔗 Share** (reproducible seed in the URL + scannable QR).

## How we built it
Pure HTML + **TensorFlow.js**, ~700 lines, no server or API — the network runs entirely
in the browser. The network is a shallow CPPN with **sinusoidal + Gaussian activations**
(the SIREN idea). Every artwork is generated from a reproducible integer **seed** via
seeded weight initialization, which is what makes sharing, Name Art, and the preset gallery
possible. Breeding and morphing operate directly on the flat weight vectors (crossover,
mutation, and linear interpolation).

## Challenges we ran into
Our first version used a deep, 9-layer, all-`tanh` network — and every image came out a
flat, washed-out blob. We discovered *why*: signal through many random `tanh` layers
**de-correlates and collapses to a constant mean**, so the output stopped depending on the
input coordinates. The fix was principled, not cosmetic: go **shallow (3 layers)** and use
**periodic activations (sin/gauss)**, which preserve high-frequency structure. That single
change is the difference between grey mush and crisp, swirling, marbled art.

## Accomplishments we're proud of
- It's genuinely *evolutionary*, not just a randomizer — the breed grid is real
  human-in-the-loop neuro-evolution.
- The SIREN insight — diagnosing and fixing the deep-network collapse.
- Everything is reproducible and shareable from a tiny seed.

## What we learned
How CPPNs and SIREN networks turn coordinates into imagery, why depth hurts random-weight
generators, and how to build a fast, fully client-side ML art tool with TensorFlow.js.

## What's next
Text-prompt guidance, a WebGL render path for 60fps, and a community gallery of shared
seeds.

---

## 🎤 60-second demo script
1. **(0:00) Hook.** "Everything you're about to see *is* a neural network. There are no
   pixels, no dataset — the image doesn't exist until the network computes it." *(Gesture
   at the live nebula.)*
2. **(0:10) Make it personal.** Type a judge's name → **Generate**. "Your name, turned
   into a one-of-a-kind neural artwork — and it's reproducible: the same name always makes
   this exact piece."
3. **(0:22) Evolution.** Hit **Breed**, pick two from history → the generation grid opens.
   Click a favorite. "This is interactive evolution — I'm the fitness function, steering
   the network through the space of everything it could paint."
4. **(0:38) Theme payoff.** Scroll to **zoom in**. "It's a continuous function, so there's
   infinite detail — no resolution, no original file. **Export HD** proves it renders at
   any size."
5. **(0:50) Share.** Hit **Share** → QR appears. "Scan this and you'll open the exact same
   artwork. This piece cannot exist without the network — that's the whole point."

## ✅ Pre-demo test checklist (run on your actual demo laptop + a phone)
- [ ] Page loads; landing art renders.
- [ ] Gallery presets, Name Art, palette, symmetry all work.
- [ ] Breed grid: select 2 → grid → click tile → Use selected.
- [ ] Morph: select 2 → animates; press Record to capture a clip.
- [ ] Zoom/pan (scroll + drag on laptop; pinch + drag on phone).
- [ ] Export HD — confirm it finishes in a couple seconds (GPU) and downloads.
- [ ] Audio React — mic permission + visible response.
- [ ] Share — QR renders, "Copy link" works, opening the link reproduces the piece.

## ✨ Framing lines (for the pitch / booth sign)
- "Every artwork is a neural network. You're not editing an image — you're steering a
  function through the space of everything it could ever paint."
- "No brush, no dataset, no pixels. The art doesn't exist until the network is asked to
  imagine it — and no two evolutions ever land in the same place."
