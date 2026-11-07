# Craft: traps, verification, house rules

## The simple version

This file is the accumulated scar tissue, and it is the one part of the kit that is
**not** open to reinvention. Everything here cost real debugging time on a previous
build, or was a correction Anshul gave once and should not have to give twice. Changing
any of it does not produce a different look — it produces a silently broken page.

Be as inventive as you like with what the site *does*; treat this file as the floor it
stands on. The traps section in particular is worth reading in full before you
write animation code, because every one of these fails *silently* — the page looks
plausible, the console is quiet, and the effect simply never happens.

Then there is the verification loop, which is the only reason those bugs were caught at
all: screenshot the page at a dozen scroll positions and look at every frame.

---

## Traps that fail silently

### A clipped element never enters the viewport

The classic word-mask reveal wraps each word in `overflow: hidden` and starts the inner
span translated fully below it. If you also put the in-view trigger on that inner span,
it will never fire — `IntersectionObserver` intersects with the clip rectangles of
ancestor elements, so a fully clipped element reports no intersection, forever.

**Fix:** put the trigger on the heading and let the children animate from parent state
(variants with `staggerChildren`). This killed every headline on the RIVR build and the
page still looked reasonable in a screenshot of the hero, because the hero used
`animate` rather than `whileInView`.

**Generalises to:** anything that starts outside its own clipping parent — sliding
drawers, curtain panels, marquee rows.

### SVG transform origin

`originX` / `originY` do not resolve reliably against a viewBox coordinate system. A
ring set to rotate around `originX: '520px'` silently rotates around somewhere else and
travels off the artboard. Use an explicit `transformOrigin: '520px 280px'` in style.

### Animating SVG geometry attributes

Animating `r`, `cx`, `x1` and friends through a JS animation library often produces
`Expected length, "undefined"` on the first frame — the library has no initial value to
read from the attribute. Either give an explicit initial, or use SMIL (`<animate>`,
`<animateMotion>`), which is declarative, cheap, keeps running while the main thread is
busy, and never fights the scroll handler.

### Non-breaking spaces in split text

Splitting a headline into `inline-block` word spans collapses the whitespace between
them — "Fluid Asset Streams" renders as "FluidAssetStreams". Emit ` ` between
words, not `' '`.

### Zero-size elements and in-view triggers

An element starting at `width: 0` or `scaleX: 0` has an empty box. Default thresholds
still fire, but any `amount` above 0 will not. Prefer animating a full-size element's
`scaleX` with `originX: 0` over animating `width`.

### Hooks inside `.map()`

`useTransform` called per item works while the list length is constant and breaks the
moment it is not. Hoist shared motion values above the map, or move the item into its
own component — which is also how you give each item its own scroll range cleanly.

### Layout thrash from animating the wrong property

Animate `transform` and `opacity`. `filter: blur()` is affordable on entrance and
expensive when scrubbed continuously across a big element. `width`, `height`, `top` and
`box-shadow` are never worth it — recreate the effect with transforms or with a scaled
pseudo-element.

### Numbers that jitter

Any counter needs `font-variant-numeric: tabular-nums` or the layout shifts on every
frame. It reads as a rendering bug even when nobody can name it.

### Pinned sections that fight smooth scroll

`position: sticky` inside a container with a transform on it stops sticking. Keep the
pin container transform-free and animate its children.

### Video that will not autoplay

`autoPlay muted loop playsInline`, all four, always. In a headless screenshot run add
`--autoplay-policy=no-user-gesture-required` or every frame shows a black rectangle and
you will misdiagnose it as a layout problem.

---

## The verification loop

Never report a site as working from reasoning alone. The loop:

1. Start the dev server on a fixed port.
2. Run a screenshot sweep — 12–14 stops desktop, 8–9 mobile.
3. **Look at every frame.** Not the first and last. The failures hide in the middle.
4. Read the console errors the sweep prints. SVG attribute errors do not surface
   visually.
5. Fix, re-sweep, re-look.

A sweep script that works (Windows paths shown; adjust the executable path):

```js
import { chromium } from 'playwright-core'
import os from 'node:os'
import path from 'node:path'

const EXE = path.join(os.homedir(), 'AppData/Local/ms-playwright/chromium-1243/chrome-win64/chrome.exe')
const OUT = process.argv[2] || '.'
const MOBILE = process.argv[3] === 'mobile'

const browser = await chromium.launch({
  executablePath: EXE,
  args: ['--autoplay-policy=no-user-gesture-required', '--mute-audio'],
})
const page = await browser.newPage({
  viewport: MOBILE ? { width: 390, height: 844 } : { width: 1440, height: 900 },
})

const errors = []
page.on('console', (m) => m.type() === 'error' && errors.push(m.text()))
page.on('pageerror', (e) => errors.push('PAGEERROR ' + e.message))

await page.goto('http://localhost:5178/', { waitUntil: 'load' })
await page.waitForTimeout(4200) // let the preloader finish

const stops = MOBILE
  ? [0, 0.08, 0.2, 0.34, 0.46, 0.58, 0.72, 0.86, 1]
  : [0, 0.06, 0.13, 0.2, 0.28, 0.36, 0.44, 0.52, 0.6, 0.68, 0.76, 0.84, 0.92, 1]

let i = 0
for (const s of stops) {
  await page.evaluate((f) => window.scrollTo({
    top: (document.body.scrollHeight - innerHeight) * f, behavior: 'instant',
  }), s)
  await page.waitForTimeout(1400)
  await page.screenshot({ path: `${OUT}/${MOBILE ? 'm' : 'd'}${String(i++).padStart(2, '0')}.png` })
}

console.log('console errors:', errors.length ? errors.slice(0, 10) : 'none')
await browser.close()
```

**Probe, do not guess.** When something looks wrong, read the actual computed state
rather than theorising — `getComputedStyle(el).transform` and `.opacity` on the element
that should have moved. That is what turned "the headlines feel off" into "no headline
has ever animated".

**A note on the browser:** the persistent playwright MCP profile is single-instance. If
it is already in use, do not fight it — a local `playwright-core` script like the one
above is faster anyway and leaves a folder of frames you can flip through.

---

## House rules

- **Native cursor, always.** Never replace or hide the pointer. Build 1 did; every build
  since has not, deliberately.
- **Every control works.** Nav scrolls, forms submit or open mail, accordions open,
  copy buttons copy, carousels advance. A dead control makes the whole page a mockup.
- **Mobile is a build, not a media query.** If a wide set piece shrinks into
  illegibility, author the upright version. Nothing overflowing is not the same as
  something working.
- **`prefers-reduced-motion` is honoured.** Skip smooth scroll, disable looping CSS
  animation, keep entrances instant. Two lines each, and it is the difference between a
  professional build and a demo.
- **Typecheck and production-build before reporting done.** `tsc --noEmit` then the real
  build. Say so plainly, with the output, and say plainly when something failed.
- **README opens in plain English.** Short sentences, one idea each, at the very top of
  the file — before the stack table, before the file list.
- **Never overwrite a previous build's folder.** If the folder name he asks for is taken
  by an earlier site, create a sibling and say so in one line.

## Calibrated defaults — tune with care

These sit between the show and the floor. They may repeat freely, because they are hands
rather than show, and they are tuned rather than arbitrary. Move one when the material
asks for it — a longer headline wants a smaller stagger, a four-beat set piece wants more
scroll, a lighter ground wants less grain — and look at the result afterwards. Do not
move one merely to be different: outside these ranges motion stops reading as expensive
and starts reading as slow or jittery, which is nobody's design choice.

- Entrance easing `[0.16, 1, 0.3, 1]`, ~0.9s, with a 10px blur that resolves.
- Springs: `stiffness 220, damping 18` for pointer-following; `90 / 28` for scrubbed
  scroll values so a fast flick does not snap.
- Stagger 0.045–0.06s per word. Below 0.03 reads as one block; above 0.08 reads slow.
- Pinned sections: 300–340vh of scroll for a build sequence with three beats.
- Grain at 0.16 opacity, `mix-blend-mode: overlay`, over anything that should feel
  physical.
- Radii that change with breakpoint, never a single fixed value.
