# amara.net

A playful, interactive single-page website built for a 3-year-old named Amara — designed to be poked at gleefully by tiny hands while being delightful for parents and family to share.

## What's on the page

The site is a single self-contained HTML file (`amara-website.html`) with no external runtime dependencies beyond a Google Font (Fredoka). Everything else — animations, sounds, games — runs natively in the browser.

### Header
- The name **AMARA** rendered as five bouncing bubble-letters, each with a multi-color gradient text fill, white drop-shadow outlines, and a staggered bounce animation
- `.net` displayed in clean black sans-serif beneath the bubbles, completing the domain branding
- A "Spin AMARA!" button positioned directly below `.net` so the spin effect is visible without scrolling

### Animated scenery
- **8 birds** flying left-to-right above the parade, each with a flapping wing animation, varied sizes, and staggered durations and heights so they feel like a flock rather than a column
- **Animal parade** scrolling right-to-left in a continuous loop: elephant (with balloon, water spray, and bobbing motion), lion, monkey, tiger, giraffe, zebra, dog, cat, platypus. The track contents are duplicated so the loop is seamless.
- **Pond** with **6 fish** (orange, purple, green, pink, yellow, blue) jumping in arcs that emerge from the water, peak above the surface, and splash back. Animated water ripples ride on the surface. Fish never escape — no flopping fish on the lawn.

### Interactive buttons
Five buttons that trigger fun effects:
- **Confetti!** — drops 50 colorful confetti pieces from the top of the viewport
- **Make animals jump!** — each animal in the parade bounces up in a wave
- **Rainbow time!** — the page background cycles through colors for 4 seconds
- **Boop!** — plays a two-tone chime
- **Spin AMARA!** (in the header) — spins each bubble letter 360° in sequence

### Games
Four small games appropriate for early ages:
1. **Pop the bubbles!** — click each colored bubble to pop it; counter tracks remaining; popping all of them triggers confetti
2. **Match the color!** — match a colored swatch to a target; new target appears after each correct match
3. **Count the stars!** — tap each star; the counter increments and confetti fires when all are counted
4. **Find the shape!** — pick the requested shape (circle, square, triangle, star); randomized each round

Wrong answers play a low tone; correct answers play an ascending two-tone chime.

### Music
A 3-voice Web Audio synthesis of "Mary Had a Little Lamb":
- **Melody** in triangle wave (the lead voice)
- **Bass** in sine wave one to two octaves below, following chord roots
- **Chord harmonies** as soft sine triads (C major, F major, G major) following a I-V-I-IV-V-I progression
- Each note has a smooth attack/release envelope to avoid clicks

The melody loops continuously when toggled on. Real MIDI files aren't supported natively in browsers, so the song is encoded as a JS data structure and synthesized in real time — works offline with no external assets.

## Structure

```
amara-website.html    # The whole site, one file
README.md             # This file
CLA.md                # Contributor License Agreement
```

Internally the HTML file is organized as:
- `<style>` block: CSS variables, animations (bounce, drift, bob, fly, ripple, fish-jump, confetti-fall), component styles
- `<body>`: header → birds → parade → pond → fun-section (buttons + games + music) → script
- `<script>`: all interactivity, audio synthesis, game state, and the symphonic melody data

## Running locally

Open `amara-website.html` in any modern browser. That's it. No build step, no server, no install.

The Google Font is loaded from `fonts.googleapis.com`; if you want it to work fully offline, download the Fredoka font and reference it locally.

## Browser support

- Chrome, Edge, Safari, Firefox — all current versions
- Audio requires a user click to start (browser autoplay policy) — the music button handles this
- Animations use CSS `@keyframes` and standard transforms; no WebGL required

## Editing

Each animal in the parade is hand-drawn SVG inline in the HTML. To modify or replace an animal, find its `aria-label` (e.g. `aria-label="zebra"`) — note that there are **two copies** of each animal in the parade-track div for the seamless loop, so changes need to be applied to both copies.

To add a new song, follow the `symphony` array structure in the script: each entry is `{ mel, dur, chord, bass }`. Frequencies are in Hz; durations in beats (1.0 = quarter note at the current tempo).

## Credits

- Font: [Fredoka](https://fonts.google.com/specimen/Fredoka) by Milena Brandao, via Google Fonts
- Everything else: original SVG art and code

## License

See `CLA.md` for the contributor license agreement. The site itself is private — built for Amara, by family.
