# Neural Canvas

**Evolve a neural network into art.** — Hack the Arts 2026 submission

Every image in Neural Canvas *is* a neural network. A **Compositional Pattern Producing
Network (CPPN)** maps each pixel's coordinates `(x, y, radius)` plus a latent vector
`(α, β, γ)` directly to an RGB color. There is no image file, no dataset, no brush — the
picture doesn't exist until the network computes it, pixel by pixel. **This art cannot
exist without the network.**

It runs entirely in your browser with [TensorFlow.js](https://www.tensorflow.org/js) —
no server, no API.

▶ **Live:** https://danny-397.github.io/neural-canvas/

## What makes it art you evolve, not just generate

- **🧬 Breed** — pick any two artworks from your history and open a **generation grid** of
  offspring (weight crossover + mutation). Click the one you like and it breeds a new
  generation from there — over and over. Human-guided neuro-evolution in the lineage of
  Picbreeder and NEAT. *Your taste is the fitness function.*
- **⚛ Mutate** — perturb the current network's weights to explore nearby variations.
- **✦ Name Art** — type any word and it's hashed into a seed, so your name always makes the
  same piece. Algorithmic authorship: the network turns language into a picture.
- **♾ Infinite zoom & pan** — because the image is a continuous *function* of coordinates,
  you can zoom in forever and new detail keeps emerging. There is no underlying resolution —
  so **Export HD** renders it at any size (2048×2048 and beyond).
- **🔷 Symmetry** — fold the coordinate field into mirror and kaleidoscope patterns.
- **🎙 Audio React** — your microphone drives the latent vector (bass → α, mids → β,
  treble → γ).
- **⏺ Record** — export the living animation as a video.
- **🔗 Share** — the exact artwork is encoded into a reproducible seed in the URL, with a
  scannable **QR code**; anyone who opens the link sees the same piece.
- **🖼 Gallery** — a set of curated showpieces to start from.

## How the network works

A compact CPPN with **sinusoidal and Gaussian activations** (the
[SIREN](https://www.vincentsitzmann.com/siren/) idea). Periodic activations — not plain
`tanh` — are what give the output its crisp, intricate structure; a deep all-`tanh` stack
collapses to a flat mean, while a shallow sinusoidal network preserves detail. Every
artwork is generated from a reproducible integer **seed**, so the same seed always
rebuilds the same network.

## Tech

Pure HTML + TensorFlow.js. Open `index.html` — that's the whole app.

Created for **Hack the Arts 2026** — *art that wouldn't exist without technology.*
