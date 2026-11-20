# NEON GRAZE

> **Don't dodge. Skim.**
> A one-file arcade game about flirting with death.

You cannot shoot. You have no gun, no bullets, no power-ups. The **only** way to charge
your weapon is to fly *close enough to die*. Every near-miss feeds the multiplier.
Every cowardly dodge starves it.

**[▶ Play it in your browser](https://anshsingh.github.io/neon-graze/)** — no install, no build step, no dependencies. One HTML file.

---

## Why it's interesting

Most arena shooters reward *avoidance*. NEON GRAZE inverts that: safety is the losing
move. The optimal play is to sit inside the danger envelope and thread the needle at the
last possible pixel. That single inversion turns a dodge-'em-up into a risk-management
game with a permanent, visible, decaying score multiplier breathing down your neck.

Three systems interlock:

| System | What it does | Why it matters |
| --- | --- | --- |
| **Graze** | Passing within 36 px of an enemy's hull builds multiplier *and* charge | The reward is literally proximity to failure |
| **Multiplier** | Rises ~0.06 per graze tick, decays 0.45/s after 1.1 s of calm | You cannot bank it — you have to keep earning it |
| **Pulse** | Spend charge for a shockwave sized by how much you charged | Banking charge = defenseless. Spending early = weak blast |

The tension is the point: **holding charge makes you fragile, spending it makes you weak.**
There is no comfortable middle.

## Feel

The whole thing is tuned for the first 3 seconds — the part that decides whether someone
plays a second run.

- **Time dilation** on every graze-adjacent pulse and on every hit, so the moment registers
- **Procedural audio** — kick, hats, bass line and arpeggio are synthesised in WebAudio and
  *layer in as your multiplier climbs*; the music is a score readout you can hear
- **Screen shake, additive particle bursts, chromatic shockwave rings, floating score pops**
- **Hue drift** — the entire palette rotates from cyan → violet → magenta → gold as the
  multiplier rises, so a hot run *looks* different from a cold one
- **Danger state** — at one life the screen edges pulse red
- **No assets whatsoever.** Every pixel is drawn with Canvas 2D, every sound is generated
  at runtime. The file is ~42 KB.

## Controls

| Action | Keyboard / Mouse | Touch |
| --- | --- | --- |
| Fly | `WASD` / arrow keys, or move the mouse | Drag anywhere |
| Pulse | `Space` / `Enter` / left click | Tap |
| Pause | `P` / `Esc` | — |
| Restart | `R` | Retry button |
| Mute | `M` | — |

Best score persists in `localStorage`.

## Run it locally

```bash
git clone https://github.com/anshsingh/neon-graze.git
cd neon-graze
open index.html          # macOS
# xdg-open index.html    # Linux
# start index.html       # Windows
```

It works straight off the filesystem — no server, no bundler, no `node_modules`.

## Deploy

Push to `main`. The included workflow (`.github/workflows/pages.yml`) publishes the repo to
GitHub Pages automatically. Then enable **Settings → Pages → Source: GitHub Actions**.

## Tech

- Canvas 2D, fixed 120 Hz physics timestep with an accumulator and interpolated rendering
- WebAudio: lookahead-scheduled 132 BPM sequencer, all oscillators + one noise buffer
- Zero runtime dependencies, zero network requests, zero build step
- Object-capped particle pool, cached glow sprites, DPR-aware canvas sizing
- Respects `prefers-reduced-motion` (disables screen shake)

## License

MIT — see [LICENSE](LICENSE).

---

*Built to be the kind of thing you open for "one run" and close forty minutes later.*
