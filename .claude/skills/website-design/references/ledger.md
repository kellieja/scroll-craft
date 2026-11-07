# The ledger

## The simple version

This is the vocabulary so far — every animation move already used for Anshul, which
site it appeared on, and **what form it took there**.

That last column is the whole point. This is not a banned list. A move that has been
used once is not used up; it is a word you now know. What it cannot do is arrive again
in the same form with different text in it. So read the form, then change the form:
what drives it, what it is made of, what it means, where it sits, how it ends. The five
axes are set out in SKILL.md under "Transform, don't retire".

Append a new section after every build, and in it say plainly how each returning move
was re-made. If you do not, this file goes stale within two projects and the skill stops
working.

---

## The four builds

| # | Site | Where | Stack | Signature move |
| --- | --- | --- | --- | --- |
| 1 | Marcus Bennet — personal portfolio | `sites/portfolio` | React 18, GSAP, Lenis, Tailwind 3 | Two-part custom cursor with retargeting labels |
| 2 | Dental Health — clinic landing page | `sites/dentist` | React 18, Tailwind 3, hand-written CSS, **no animation library** | Booking drawer that slides from the right and confirms with a tick |
| 3 | Viktor Davies — designer portfolio | `designer-next-award-portfolio` | React 19, GSAP, Lenis, Tailwind 3 | Project list playing a video that follows the pointer |
| 4 | RIVR — DeFi protocol site | `rivr-next-award-portfolio` | React 19, `motion/react`, Lenis, Tailwind 4 | A flow diagram that assembles itself across a 320vh pin, with liquidity travelling the channels |

---

## Vocabulary: entrances and text

| Move | Sites | The form it took |
| --- | --- | --- |
| Preloader counting 0→100 | 1, 2, 3, 4 | Centre-screen numeral with a hairline progress rule |
| Preloader exit | 3, 4 | 3: splits open. 4: lifts on a curved bottom edge |
| Preloader word swap | 4 | Three synonyms cycling in place while the count runs |
| Headline rising letter by letter | 2, 3 | 2: with skew. 3: straight, from a clip mask |
| Headline rising word by word | 4 | Behind a per-word clip mask, staggered 0.055s |
| Scramble / decode text | 1 | Glyph cycling on entry, monospace |
| Typewriter reveal | 1 | Character append with a caret |
| Word opacity scrubbed by scroll | 4 | Faint → solid across a 90vh section, one long sentence |
| Blur-to-sharp entrance | 4 | 10px blur resolving alongside a 28px rise |

## Vocabulary: numbers and data

| Move | Sites | The form it took |
| --- | --- | --- |
| Count-up on first view | 1, 2, 3, 4 | Static end value, quartic ease, one shot |
| Rolling digit columns | 4 | Per-digit swap on a live price changing every 1.6s |
| A number that never stops | 4 | rAF-incremented streaming balance to four decimals |
| Chart drawn with `pathLength` | 4 | Sparkline plus a gradient fill area, once on entry |
| Progress / capacity bars | 4 | `scaleX` from `originX: 0`, re-running on tab change |
| Live clock | 2, 4 | 2: local time under an emergency line. 4: UTC in the footer |

## Vocabulary: scroll behaviour

| Move | Sites | The form it took |
| --- | --- | --- |
| Lenis smooth scroll | 1, 3, 4 | ~1.15s duration, exponential ease |
| Top progress rail | 3, 4 | Full-width hairline, `scaleX` from left |
| Velocity-reactive marquee | 1, 4 | Words; direction flips with scroll sign. 4 adds skew |
| Pinned scrubbed build sequence | 4 | 320vh, SVG diagram assembling in three beats |
| Horizontal rail from vertical scroll | 3, 4 | Cards translating on X, progress bar in the header |
| Hero video parallax | 4 | Scale 1→1.18 plus 8% drift, veil darkening over it |
| Nav that hides down / returns up | 2, 3, 4 | 2, 3: the real bar. 4: a separate glass dock after the hero |

## Vocabulary: pointer and hover

| Move | Sites | The form it took |
| --- | --- | --- |
| Magnetic buttons | 1, 3, 4 | 0.25–0.35 strength, spring 220/18 |
| 3D tilt cards | 2, 4 | ±6–8°, with a radial sheen tracking the pointer |
| Video following the pointer | 3 | Over a project list, one shared player |
| Pointer-parallax floating chips | 4 | Glass chips drifting against pointer on the hero |
| Greyscale → colour | 2 | On hover, over a results gallery |
| Label roll on hover | 2 | Two stacked copies, the pair sliding 130% |

## Vocabulary: structure and surface

| Move | Sites | The form it took |
| --- | --- | --- |
| Inset card with big radii | 2, 3, 4 | Page ground framing it via `p-3 md:p-5` |
| Dark closing card | 2, 4 | **2: flat black, one white blur orb, live emergency line — the one he singled out.** 4: hero film under a navy veil |
| SVG faux corner cut-outs | 4 | Two 56px masks turning a rectangle into a cut shape |
| Glass over moving media | 4 | `bg-white/30 backdrop-blur-xl` over video only |
| Film grain | 4 | 0.16 opacity, `mix-blend-mode: overlay` |
| Bento grid | 4 | Six cards, mixed spans, one inverted to navy |
| Height-animated accordion | 3, 4 | 3: service rows. 4: FAQ with a rotating plus |
| Shared-layout pill (`layoutId`) | 4 | Behind a three-way vault selector |
| Quote carousel | 3, 4 | Auto-advancing with directional blur transitions |
| Drifting logo band | 4 | Linear loop with gradient edge fades |
| Page-wide wordmark | 4 | 24vw, gradient-clipped, scaling in as the footer arrives |
| Slide-in drawer with a form | 2 | From the right, name + phone, tick on success |

## Not a technique — a standing house rule

| | |
| --- | --- |
| **Custom cursor** | Built once, on site 1 (two-part dot and lagging ring). Do not build another. The native pointer stays visible and unmodified — pointer-*reactive* elements are welcome, a pointer *replacement* is not. |

---

## Room still wide open

Not a to-do list — a reminder of how much is left before variation is even needed.
Details and how-to in `moves.md`.

Canvas or WebGL of any kind · shader-style displacement · particle or fluid fields ·
image-sequence scrubbing · CSS `animation-timeline` scroll-driven animation ·
`clip-path` morphing between shapes · SVG filter goo / gooey merge · SVG `feTurbulence`
displacement on hover · variable-font weight animating on scroll · text set on a curved
path · FLIP shared-element transition carrying an image between two sections ·
sticky stacking cards that overlap as you scroll · a page ground colour that travels
through the palette section by section · split-flap / departure-board type ·
dither, halftone or ASCII transitions · CSS `mask-image` wipe reveals ·
`mix-blend-mode: difference` overlays that invert over media · 3D CSS carousel or
perspective corridor · physics springs with real overshoot and settle ·
audio-reactive or time-of-day-reactive states · a live mini-tool the visitor can use ·
scroll-driven SVG morph between two logos · cursor-driven light source on a 3D-lit card

---

## Add the next build here

Use this shape:

```markdown
## N — <site name> (<date>) — `<folder>`

Stack: ...
Signature move: <one sentence>
New to the ledger: <what had never been done before>
Brought forward and re-made: <each returning move, and which axes changed>
Tried and rejected: <what did not work, and why — the most valuable line in the entry>
```

---

## 4 — RIVR (2026-09-03) — `rivr-next-award-portfolio`

Worked example of the shape above, so the next entry has something to copy.

Stack: Vite 7, React 19, TypeScript, Tailwind 4, `motion/react`, lucide-react, Lenis.

Signature move: a flow diagram that assembles itself across a 320vh pin — three idle
assets appear, channels draw between them, a vault ring spins up, and blobs of
liquidity travel the channels into "Liquid cash", with the caption swapping on three
beats.

New to the ledger: the pinned self-assembling diagram; SMIL `animateMotion` for the
travelling liquidity; rolling per-digit columns on a live price; an SVG area chart drawn
with `pathLength`; a `layoutId` pill behind the vault selector; SVG faux corner cut-outs.

Brought forward and re-made:
- *Dark closing card* (from Dental Health) — changed **what it is made of**: the hero
  film under a navy veil instead of flat black, so the page closes on the image it
  opened with. Changed **what the live element means**: a streaming counter, not a
  clinic clock.
- *Count-up stats* — changed **what they mean**: one of them never stops counting,
  because a protocol that pays by the second should not show a number that settles.
- *Velocity marquee* — changed **how it ends**: added skew tied to scroll velocity so
  the whole band leans, rather than only changing speed.
- *Horizontal rail* — changed **where it sits**: it now terminates on an open dashed
  card that hands off to the CTA instead of simply running out.

Tried and rejected: `originX`/`originY` for the rotating vault rings (silently wrong
origin, rings flew off the artboard — replaced with explicit `transformOrigin`);
per-word `whileInView` triggers (never fire inside a clip mask — moved to parent
variants); animating SVG `r` through motion (undefined on first frame — moved to SMIL);
the wide diagram on mobile (legible in theory, unreadable at 390px — authored a separate
upright version).

---

## 6 — LGPSM (2026-09-15) — `lgpsm-fashion`

A pure-white minimal futuristic fashion site, built from an exact pixel-spec hero brief
(fonts, fluid clamp() variables, background URLs, a canvas-driven mouse-reveal effect,
four drawers with real cart/checkout behaviour). First build in the ledger with **no
grey/dark palette at all** — everything before this alternated dark and light; this one
never leaves white-on-black-text except for two intentional full-bleed black bands.

Stack: Vite 8, React 19, TypeScript, Tailwind 4, `motion/react`, lucide-react. No Lenis —
native scroll, since the signature piece needed real `document.scrollHeight` to pin
against.

Signature move: **the Scan Series** — a 320vh pinned section where four garments slide
past horizontally as you scroll vertically, each card carrying a HUD-style spec sheet
(material/weight/build) instead of a product photo, with faint corner-bracket "targeting"
marks that sharpen on hover. It closes on a fifth, dashed-border card — "VIEW FULL
ARCHIVE" — that hands off to the shop drawer rather than just running out of cards.

New to the ledger:
- A **spec-sheet card** standing in for product photography entirely — the brief supplied
  only two hero images, so garment "photos" became schematic data instead of inventing
  fake product shots.
- **A canvas-generated cursor-reveal mask** (`mask-image` built from `toDataURL()` every
  frame) — the hero's second background image is only visible inside a soft radial
  spotlight that eases toward the cursor at 0.1, with a parallax SVG grid underneath.
- **Client-measured pin distance.** `ScanRail`'s horizontal travel is
  `scrollWidth - clientWidth` read live off the DOM in a `ResizeObserver`-free effect, not
  a guessed percentage — see "Tried and rejected" below for why that mattered.

Brought forward and re-made:
- *Horizontal rail from vertical scroll* (3, 4) — changed **what it means**: on 3/4 it was
  a project list or a diagram; here it's a "scan" of garments, spec-sheet HUDs standing in
  for photography. Changed **how it ends**: a dashed hand-off card, the same primitive
  RIVR used, re-made again by an open button instead of an open link.
- *Count-up on first view* (1,2,3,4) — unchanged mechanically, `tabular-nums` and a
  quartic ease; only the numbers themselves (drops shipped, countries, recycled %) are
  new.
- *Inset/bordered cards, big radii* — changed **material**: hairline borders only, no
  fill, no shadow at all (the brief explicitly banned "cards-as-decoration"), corner
  brackets standing in for the radius-driven framing every other build used.

Tried and rejected:
- **A pinned rail sized only by card `min-width` clamps.** With 4 cards at a modest width
  the total `scrollWidth` barely exceeded the viewport — a 320vh pin that translated the
  track a grand total of 98px. Looked fine in a static screenshot of the first frame and
  was almost inert in motion. Fix: measure the actual DOM distance, widen the cards, and
  add a fifth closing card — verified afterward with `getComputedStyle(track).transform`
  sampled across the scroll range, not by eyeballing it.
- **The hero's mouse-reveal background as `position: fixed`.** Correct for a single-
  viewport hero-only page (the original brief); once the page grew a body below the hero,
  `fixed` kept the model's face bled through every section underneath it for the whole
  scroll. Changed to `absolute` inside the hero's own `relative overflow-hidden` wrapper.
- **The Unicode ring character "˚" as the wordmark's degree mark.** Orbitron doesn't carry
  that glyph; small (header logo) it rendered as a passable-looking dot, but at the
  footer's large display size it was an unmistakable browser tofu box. Replaced with a
  two-line SVG circle (`DegreeMark`) used everywhere the mark appears.
- **A generic `getByRole('button', {name:'Add'})` locator while verifying the cart flow.**
  Matched the product-grid's own "ADD" button (case-insensitive substring) instead of the
  drawer's, which was hidden behind the backdrop and produced a pointer-interception
  timeout. Scoped the query to the dialog by its `aria-label` instead.
