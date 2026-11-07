# The move catalogue

## The simple version

This is the reserve — raw material for when you need something genuinely new. Almost
none of it has been shipped for Anshul yet.

**Come here second, not first.** The stronger play is usually to take a move you already
know and re-make it for this subject: change what drives it, what it is made of, what it
means, where it sits, how it ends. A familiar mechanism given a new job reads as
*design*. An exotic mechanism half-built reads as a demo. RIVR's best section was an
ordinary pinned scroll with an idea inside it, not a rare library.

So use this file when variation has genuinely run dry, when a subject calls for something
specific here, or when you want one unmistakable thing on the page that nobody has seen.

Read it the way a designer reads a materials library: not to pick one item and be done,
but to find two that have never been put together. Each entry says what it is, why it
lands, and roughly how it is built.

---

## 1. Set pieces — one of these carries a whole site

**Self-assembling diagram.** The page pins and a system draws itself: nodes appear,
channels connect, something travels the channels. *Why it lands:* it explains the
product instead of decorating it. *How:* a tall section, `useScroll` over it, map
progress onto `pathLength`, opacity and scale of SVG groups; SMIL `animateMotion` for
the things that travel. **(Used on RIVR — vary the topology, not just the labels.)**

**Exploded view that reassembles.** Product or interface parts float apart in space,
then snap together as you scroll. *Why:* it makes something feel engineered. *How:* 3D
CSS transforms on layered PNGs or divs, `translateZ` and `rotateY` scrubbed by progress.

**One long line that becomes everything.** A single stroke drawn across the whole page
that turns into a chart, a route, a signature, a horizon, a graph. *Why:* it gives a
scattered page one continuous spine. *How:* one SVG fixed behind the content, `pathLength`
scrubbed by page-level scroll progress, waypoints that fade in as it passes them.

**Image-sequence scrub.** A short clip exported as frames, drawn to a canvas, the frame
index tied to scroll. *Why:* the most convincing "this is expensive" effect there is.
*How:* preload frames, `ctx.drawImage` on a scroll-driven index. Costs bandwidth; use 60
frames at moderate width, not 200.

**Sticky stacking cards.** Each section sticks and the next slides over it with a shadow
and a small scale-down of the one beneath. *Why:* turns a list into a deck. *How:*
`position: sticky` per card, `top` increasing per index, scale driven by that card's own
progress.

**A live tool.** A working calculator, configurator, comparison slider, or estimator
built into the page. *Why:* nothing else converts attention like something that answers
about *them*. *How:* plain state; animate the result, not the inputs.

**Colour travel.** The page background moves through the palette as you scroll, section
to section, so the site feels like a journey rather than a scroll. *Why:* it changes the
emotional temperature without a single new asset. *How:* one motion value on `body`
background driven by page progress; keep the ink colour switching in step so contrast
never breaks.

**Perspective corridor.** Content laid out in Z, so scrolling flies through it. *Why:*
almost nobody does it well and it is unmistakable. *How:* a parent with `perspective`,
children at increasing negative `translateZ`, scroll mapped to camera Z.

---

## 2. Type

- **Variable-font weight on scroll** — a headline that thickens as it enters. Needs a
  variable font; animate `font-variation-settings`.
- **Text on a curved path** — `<textPath>` on an arc, rotating slowly, or scrubbing its
  `startOffset` on scroll.
- **Split-flap / departure board** — each character cycles through glyphs and lands.
  Reads mechanical and expensive; good for stats and dates.
- **Mask wipe** — reveal by animating `mask-image` (a gradient or a shape) rather than
  by moving the text. Softer and less "web" than a clip.
- **Line-height bloom** — lines spread apart on entrance and settle. Subtle, unusual.
- **Two-layer difference type** — the same word in `mix-blend-mode: difference` over
  moving media, so it inverts as the video passes under it.
- **Kerning collapse** — letters start wide-tracked and pull to their real spacing.
- **Word-swap in place** — one noun cycles through synonyms on a timer, everything else
  static. Cheap, and it holds the eye.

## 3. Reveals and transitions between sections

- **FLIP hand-off** — an image in section A becomes the hero image of section B,
  travelling between them. Measure both rects, animate the delta, swap.
- **Curtain wipe with a curved edge** — the incoming section arrives with an animated
  `border-radius` on its leading edge, so the seam is a curve not a line.
- **Clip-path morph** — a circle opening into a rectangle, a diagonal sweeping through.
- **Gooey merge** — SVG `feGaussianBlur` + `feColorMatrix` so two shapes fuse as they
  approach. Very distinctive; use once.
- **Dither / halftone crossfade** — an image resolving from dots into itself. Canvas or
  an SVG filter. Reads retro-technical.
- **Scale-and-blur pass-through** — the outgoing section scales up and blurs while the
  incoming one scales down into place, as if the camera moved through it.

## 4. Pointer without replacing the cursor

The native pointer stays. Everything here reacts *around* it.

- **Light source** — a card lit by a radial highlight tracking the pointer, with the
  shadow on the opposite side moving in step.
- **Displacement on hover** — SVG `feTurbulence` + `feDisplacementMap` whose scale rises
  under the pointer, so an image ripples like water.
- **Repel / attract grids** — a field of dots that pushes away from the pointer.
- **Trail of ghosts** — the last N pointer positions drawn as fading shapes.
- **Elastic drag** — a card that can be thrown and springs back, with real overshoot.
- **Proximity type** — letters that thicken or lift as the pointer nears them.
- **Tilt with parallax layers** — foreground, midground and background inside one card
  moving at different rates, not the whole card tilting as one plane.

## 5. Media

- **Duotone → full colour** on scroll, using an SVG `feColorMatrix` rather than a CSS
  filter, so the midtones stay right.
- **Masked video type** — video playing inside letterforms via `background-clip: text`
  or an SVG mask.
- **Playback rate tied to scroll velocity** — the film speeds up when the page does.
- **Object-position drift** — slow pan inside a fixed frame; cheaper than parallax and
  often better.
- **Video wall that resolves** — nine tiles that shuffle then lock into one image.
- **Aspect morph** — a 16:9 frame that grows into a full-bleed panel as it centres.

## 6. Data and numbers

- **Sparkline that redraws on interaction**, not just on entry.
- **Radial gauges** drawn with `pathLength` and a needle with spring settle.
- **Stacked bars that reorder themselves** when a filter changes, animated with
  `layoutId` so bars travel to their new positions.
- **A number that reacts to the visitor** — items in view, seconds on page, their local
  time. Makes the page feel awake and costs nothing.
- **Live-ish feed** — rows entering at the top and pushing the list down, with the
  leaving row fading at the bottom.

## 7. Layout ideas that are not a bento grid

- **Editorial column breaks** — a full-bleed image interrupting a text column, the text
  resuming beneath it.
- **Off-grid overlap** — a card deliberately hanging over the section boundary above it.
- **Marginalia** — small notes in the outer margin that animate in beside the paragraph
  they belong to.
- **Ticket / stub shapes** — perforated edges via repeating radial gradients.
- **Diagonal sections** — a `clip-path` skew across a full-width band, with content
  counter-rotated so type stays level.
- **Index page** — a table of everything on the site, hover-previewed. Reads confident.

## 8. Sound and time

- **Time-of-day states** — the palette shifts toward evening after dark, using the
  visitor's clock. Announce it with one small line so it does not read as a bug.
- **Optional sound toggle**, off by default, driving small UI ticks. Only where it fits
  the brand, and never autoplaying.

---

## How to choose

Three questions, in order:

1. **What is true about this subject that no competitor could claim?** The set piece
   should dramatise that one thing.
2. **What has he not seen?** Cross-check `ledger.md` honestly. "Similar but with
   different content" counts as seen.
3. **What can be built well in the time available?** One set piece executed cleanly
   beats three half-built ones — a stuttering canvas reads cheaper than no canvas.

Then note in the ledger what you considered and rejected. Next time that list is a head
start.
