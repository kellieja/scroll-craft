---
name: website-design
description: Build a complete, heavily animated premium website - hero section, landing page, portfolio site, product or marketing site - from a brief, a design spec with exact classes, a screenshot, or a rough idea. Use this whenever the user says build this website, build this hero, make me a landing page, finish this into a full site, add more animation, make it more premium, make it feel expensive, or hands over a component spec to reproduce. Also use it when they say a build looks like a template, looks like the last one, or asks for something that will surprise them. Covers the build process, the palette and layer language, the motion catalogue, the technical traps that silently kill animations, the screenshot verification loop, and the ledger of moves already shipped that the next build has to beat.
---

# Website design

> **Where this comes from.** Written by Anshul ([@anshul09-hub](https://github.com/anshul09-hub)) from the premium websites he builds with Claude Code. Where the text says "Anshul" or "he", it means the person the site is for: read it as *you*. `references/ledger.md` is his build history. It is there so your agent re-makes moves instead of repeating them. Start appending your own builds to it.

## The simple version

This is how to build Anshul a website that moves.

Four of these exist already: Marcus Bennet, Dental Health, Viktor Davies, RIVR. Each
one was better than the last. That is the whole point of this skill — not to give you a
template to fill in, but to stop you rebuilding the fourth site a fifth time.

So the rule that matters most here: **before you build, read the ledger of what has
already been used — then re-make it rather than re-run it.** The moves are not used up.
They are a vocabulary, and a vocabulary is meant to be spoken again in new sentences.
What is forbidden is copy-paste: lifting a component across with new text in it.

The test is simple. If Anshul can look at a section and name the old site it came from,
the build has failed even if every pixel is clean.

The other half of that freedom is knowing where it stops. Some of what is written down
here is show — meant to be changed every time. Some of it is floor — bugs already paid
for, corrections already given once — and changing that does not produce a different
look, it produces a silently broken page. "What to change, what to leave alone" below
draws the line, with a single question that sorts nearly every case.

Everything else in this file is in service of that: how to plan the sections, what to
reach for when you need a new idea, the bugs that silently kill animations, and how to
prove with your own eyes that the thing actually moves.

---

## Read these before you write code

| File | When |
| --- | --- |
| `references/ledger.md` | **Always, first.** What the four past builds already used, and what has never been tried. |
| `references/moves.md` | The reserve, for when variation has genuinely run dry. Most of it has never been shipped for him. |
| `references/craft.md` | Before and during the build. The traps, the verification loop, the house rules. **This file is the floor — read it as fixed, not as suggestions.** |

`ledger.md` is a living file. You append to it at the end of every build. A skill that
does not update its own memory will repeat itself within two uses.

---

## The process

### 1. Take the brief literally, then go past it

Anshul often hands over an exact spec — class strings, hex values, a video URL, the
markup of a hero. **Reproduce that part verbatim.** Every class, in order. He checks.
When he gives you `object-[65%] lg:object-center`, that is not a suggestion.

Then build the rest of the site around it. He has never once wanted only the hero. The
brief is the opening bar, not the song. Assume ten to fourteen sections unless he says
otherwise, and assume the site has to work as a finished product: real copy, working
buttons, a real footer.

Add motion *around* specified markup — a parallax wrapper, a scroll cue, floating chips
— rather than editing the classes he gave you. That way fidelity and ambition do not
fight.

### 2. Decide the signature move before you decide the sections

Most sites are a list of sections with animations bolted on. That reads as a template.

Instead, pick one idea that only this site could have, and let the section list grow out
of it. RIVR's was a diagram that assembled itself while the page held still — three idle
assets, channels drawing, liquidity travelling into cash. That one idea justified a
320vh pin and gave the whole page a spine.

A good signature move:

- says something true about the subject (a DeFi protocol should *flow*, a dentist should
  feel *calm and clean*, a designer's portfolio should show *work*, not adjectives)
- takes a whole screen and holds it for several seconds of scroll
- cannot be dropped into the next project without looking stolen

Write the signature move down in one sentence before you open an editor. If you cannot,
you do not have one yet, and the site will come out generic.

### 3. Structure

A shape that has worked, to vary rather than copy:

`preloader → hero (the spec) → a band that breaks the grid → proof in numbers →
THE SIGNATURE SET PIECE (pinned) → the offer, interactive → a bento or layered grid →
a scroll-scrubbed statement → a second pin that moves differently from the first →
human voices → questions → closing panel that echoes the hero → footer with the wordmark`

Two rules about rhythm, which matter more than the list:

- **Alternate the direction of travel.** Down, then sideways, then pinned-still, then
  down again. Three vertical fade-ups in a row is when a page starts to feel long.
- **Alternate weight.** A dense interactive section then a near-empty one with a single
  sentence. Silence is what makes the loud parts land.

### 4. The layer language

He has asked for this by name — "the curvy vibe, more layers":

- Big radii, and *different* radii at different breakpoints
  (`rounded-[1.5rem] md:rounded-[3rem]`). Small radii read cheap.
- Full-bleed cards inset from the page edge by `p-3 md:p-5`, so the page ground shows
  as a frame around the content. It reads as a physical card on a desk.
- Real glass: `bg-white/30 backdrop-blur-xl` over moving media, never over flat colour —
  glass with nothing behind it is just a grey box.
- Faux cut-outs. Two small SVG corner masks turn a rectangle into a shape that looks
  cut from the card behind it. This is the highest-value trick in the whole kit and it
  costs twelve lines.
- A grain overlay at ~0.16 opacity, `mix-blend-mode: overlay`. It is the difference
  between "CSS gradient" and "material".
- Layer count: aim for four readable depths on the hero — film, veil, grain, glass.

### 5. Palette

Unless a brief says otherwise, hold whatever palette he set and do not drift. For the
blue family he has confirmed twice: navy `rgba(30,50,90,*)` for ink and solids, light
blues `#8fb8e8` `#cfe3f7` `#eaf2fb` for grounds and glows, white for cards, `#f0f0f0`
for the page. Opacity does the tonal work; do not introduce a fifth hue to get contrast.

### 6. Build, then verify with your own eyes

Non-negotiable, because it has caught real failures: run a screenshot sweep at 12–14
scroll stops on desktop and 8–9 on mobile, and *look at every frame*. On the RIVR build
this is how it emerged that not a single headline was animating in — the page looked
fine to reason about and was broken in fact.

`references/craft.md` has the sweep script and the checklist. Also read the console
errors it prints; SVG attribute errors are silent in the browser and fatal to a set piece.

### 7. Write the README the way he reads

Plain-English section at the very top of the file. Short sentences, one idea each. What
it does and what he has to decide, before any stack table or file list. Then the detail
underneath for whoever wants it.

### 8. Close the loop

Append to `references/ledger.md`: the site, the stack, the signature move, every named
technique, and — most usefully — what you tried that did not work. Then the next build
starts from a real memory instead of a blank page.

---

## Transform, don't retire

This is the part Anshul asked for explicitly, so treat it as the acceptance criterion
rather than as advice. And read the framing carefully, because the obvious reading is
the wrong one.

**A move that has been used is not spent. It is vocabulary.** Banning techniques after
one outing would empty the toolbox in a year and push every site toward whatever is left
over rather than whatever is right. The failure he is guarding against is not *reuse* —
it is **copy-paste**: the same component lifted across with new text in it.

So the rule is:

> Every element you bring forward from a previous build must be **re-made for this
> subject** — changed in what drives it, what it is made of, or what it means. And every
> build ships at least one move that is genuinely new to the ledger, carrying the
> signature set piece.

### The worked example he pointed at

The Dental Health site ends on a black card with big soft radii, inset from the page
edge so the ground frames it, one white blur orb bleeding off the corner, a giant
headline splitting in character by character, a white magnetic pill whose label rolls
over on hover, and a live pulsing dot reading "Emergency line open · local time". He
loves that block, and the reason is worth naming: it is not an unusual technique. It is
an inset rounded card. What makes it land is that every layer inside it was chosen for a
dental clinic — the calm black, the *chair* you are booking, the emergency line that is
actually open right now.

RIVR closes on the same primitive: inset card, big radii, giant headline, magnetic
button. Nobody would call them the same section, because the card holds the hero film
under a navy veil instead of flat black, and the live element is a streaming counter
rather than a clock. Same skeleton, different animal. That is the target.

### The five axes — how to re-make a move

When you reach for something from the ledger, change it on at least two of these:

1. **What drives it.** Time → scroll position → pointer distance → a data value →
   viewport entry → an interaction. A count-up on entry and a number driven by scroll
   velocity are not the same component in any way the viewer can perceive.
2. **What it is made of.** Text → SVG path → image → video → canvas → live DOM. A
   marquee of words, a marquee of logos, and a marquee of thumbnails that scrub on
   hover are three different sections.
3. **What it means.** The strongest axis, and the one usually skipped. A counter on a
   clinic counts *patients treated*; on a protocol it counts *value streaming right now*
   and never stops. Tie the number to something true about the subject and it stops
   reading as a widget.
4. **Where it sits and what shape it is in.** Full-bleed vs inset card, horizontal vs
   vertical, one big instance vs nine small ones, straight vs on a curved path.
5. **How it ends.** Most reused components are reused with their exit intact. Change the
   exit — settle with overshoot, hand off to the next section, leave a residue behind,
   invert.

### Your three most-worn primitives

The odometer counter, the velocity marquee and the magnetic button appear in all four
sites. They are good and they can stay. But they are the ones most likely to arrive
unexamined, so when one shows up, spend a minute on the axes above before you write it —
and say in the ledger entry how this build's version differs. If you cannot answer that,
you copy-pasted.

### Where genuinely new material comes from

- *New is not a new library.* Swapping GSAP for `motion` changes nothing he can see.
  Judge novelty by what appears on screen, never by imports.
- *Steal from outside web design.* Title sequences, instrument panels, print layout,
  transit maps, trading terminals, physical mechanisms.
- *Look before you build.* Awwwards, Godly, the 21st.dev registry, Codrops, studio
  sites. Pull two or three specific ideas and note them in the ledger even if you do not
  ship them — that list becomes next build's head start.
- *`references/moves.md` is the reserve*, not the first stop. Variation on what you know
  usually beats reaching for something exotic you will only half-build.

---

## What to change, what to leave alone

The instruction to re-make everything has an obvious failure mode: treating *all* of it
as fair game, changing something load-bearing to look inventive, and shipping a site
that is fresh and broken. Freedom applies to the show. It does not apply to the floor
the show stands on.

One question sorts almost every case:

> **If I change this and I am wrong, what happens?**
>
> - "It looks different, and he can tell me he prefers the other one" → **change it
>   freely.** That is the show, and holding it still is the actual risk.
> - "It silently stops working, or he has to correct me on something he already
>   corrected once" → **leave it.** That is the floor, and there is no creative credit
>   in rediscovering a bug.

### Free — vary these every single build

The signature set piece · the section list and its order · which moves come forward and
what drives them · materials, shapes, and where things sit · every exit · the copy ·
section transitions · the layout system · the palette when he has not specified one ·
the stack.

Nothing here can break by being changed. If a build feels like the last one, it is
because one of these was left on the default.

### Tune with care — adjust for a reason, verify after

These are calibrated, not arbitrary. Move them deliberately and look at the result;
do not move them just to be different.

Entrance ease `[0.16, 1, 0.3, 1]` and ~0.9s duration · springs 220/18 for pointer,
90/28 for scrubbed scroll · stagger 0.045–0.06s per word · 300–340vh per pinned build
sequence · grain at 0.16 · blur amounts on entrance.

Sensible reasons to move them: a longer headline needs a smaller stagger or it drags; a
four-beat set piece needs more scroll than a three-beat one; a light ground needs less
grain. Bad reason: variety for its own sake. Off the calibrated range, motion stops
reading as expensive and starts reading as *slow* or as *jittery*, and neither of those
is a look anyone chose.

### Fixed — changing these is how a build gets broken

**The brief, verbatim.** Class strings, hex values, asset URLs, markup he supplied.
Animate around them, never through them.

**Everything in `craft.md` under "traps".** Those are not style opinions, they are bugs
that were paid for once. Putting an in-view trigger back inside a clip mask, or
`originX` back on an SVG ring, does not produce a different look — it produces nothing
at all, silently, and the page still screenshots as plausible.

**The house rules.** Native cursor. Every control does something real.
`prefers-reduced-motion` honoured. Mobile authored, not just non-overflowing. Typecheck
and production build before saying done. Plain-English README at the top of the file.
Never overwrite a previous build's folder.

**The verification loop.** Sweep, look at every frame, read the console. When a build
runs late this is the first thing that feels skippable, and it is the one step that has
actually caught silent failures.

**Semantics and contrast.** Heading order, focus states, alt text, text that stays
readable over media.

### The rule underneath all of it

**Newness is additive. Never buy it by removing a guarantee.** Dropping reduced-motion
support, skipping the sweep, or leaving a button dead to save time for a flashier
section is not a trade — it is the one kind of change he will always notice, and the
kind he should never have to ask about twice.

---

## What good looks like

He has told you, across four builds, what he actually judges:

- **It moves, and the movement means something.** Motion that decorates gets noticed as
  motion. Motion that explains gets noticed as quality.
- **Every button does something real.** Menus scroll. Forms submit or open mail. Toggles
  toggle. Copy buttons copy. Dead controls on a beautiful page read as a mockup.
- **His mouse pointer is his.** Never replace or hide the native cursor. The first build
  did; every one since has not. Pointer-reactive elements are welcome — a replacement
  pointer is not.
- **It holds up on a phone.** Not "does not break" — holds up. A wide diagram shrunk to
  390px is a failure even though nothing overflowed; build the upright version.
- **Nothing in the console.** Zero errors across the sweep, at every stop.
