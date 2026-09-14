# Mobile Guided Path

EchoPark VDP 2.0 · SA-0777 · mobile expansion of the desktop guided-path work

## Start here — `index.html`

**`index.html` is the primary build.** Everything reviewed from 28 August onward lives here, and
it is the only file that carries the current design decisions. Open it and use the phone; the
controls panel on the left picks an entry variant, a comparison concept, and any single state.

`?state=` deep-links every screen — `index.html?state=P3.C4` opens Concept C's results table.
`state-board.html` indexes all 47 states with a one-line note on each.

### What it carries

**The three guided questions** — What will I pay? · Does it fit my needs? · How does it compare? —
reachable from five switchable entry treatments:

| Variant | Treatment | Notes |
|---|---|---|
| B · toast | a real toast above the sticky bar, at 2.5s | taps through to the drawer |
| C · price | a callout inside the price block | no "Help me decide" row — it would be redundant |
| D · persistent nav | a bar revealed once the hero scrolls past | |
| D2 · nav + price | as D, with identity and price in the left slot | same component as D, different label |
| A · bar | a panel in the page | **the only variant that does not use the drawer** — its row expands the panel in place and collapses back |

Every variant except A routes into one shared drawer. "Help me decide" is permanent and is the
single control that opens it.

**What will I pay?** opens answer-first — the total at full size, then three doors into the cost
breakdown, protection plans, and terms/prequalification. The pay-path shape (layers vs one
scroll) is switchable in the panel while the sheet is open.

**Does it fit my needs?** — the Chat with Echo conversation from Figma `1:3201`. Earlier turns
fold to a one-line summary so the conversation stays about a screen however long it runs.

**How does it compare?** — three concepts, ported from `car-comparison-mobile-concepts/`:

| | Screen 1 | Screen 2 | Screen 3 | Screen 4 |
|---|---|---|---|---|
| **A · Full-screen sheet** | Empty | One added | Two added | Results |
| **B · Ask Echo search** | Prompt | Ranked | Two added | Results |
| **C · Ask Echo conversation** | Echo opens | Road trip | Cargo room | Results |

A is the control — the desktop modal translated straight down, no AI. Its results table carries
no "Echo's take" row and picks no winner, because A has no Echo to have an opinion. That contrast
is the argument for B and C.

### Conventions this build holds to

- **Greyscale.** No colour anywhere; the remap is one block at the end of `styles.css`, so
  restoring colour is deleting it. Every link is underlined, since colour is no longer marking
  them.
- **Icons at 18 × 18.** Two deliberate exceptions: the selection check is 13 × 9 per
  `selection-check.svg`, and the price-drop arrow keeps its 24px disc.
- **No hover on touch.** Hover rules live in `@media (hover:hover) and (pointer:fine)`; touch gets
  `:active` press feedback instead. Add hover rules inside that block.
- **Swipe, not arrows.** The hero and the full-screen viewer both swipe; counters stay.
- **One photograph, in the hero only.** `GALLERY_PHOTOS` is the flag; everything else is a plain
  block until real photography arrives.
- **Panel controls are inert outside the scenario they affect** — dimmed and unclickable.

## Reversed along the way

Two things were built and then taken out, both correctly:

- **The reassurance strip** — 190-point inspection, 7-day return, free CARFAX, 30-day warranty in
  the price block. Those details are not above the fold on desktop, and mobile should not invent a
  different information hierarchy.
- **A bespoke prequalification screen** inside buying options. The desktop treatment already
  handled the entry; what survives is the part that was right — the prequalification view itself
  is owned by another team, so the prototype hands off and says so.

## `vdp.html` — historical, do not build on it

`vdp.html` is the DS-native prototype with the first guided-path layer grafted on. It was the
primary build for one day. **It stopped at 28 Aug 12:59 and has none of the work since** — no
greyscale, no 18px icons, no swipe, no drawer, no price-block rework, no comparison concepts. It
is kept for reference only. If you find yourself editing it, you are in the wrong file.

## Competitive position

CarMax's mobile VDP measures ~11.5 screens; Carvana's ~8.5+ and truncated. The preferred one is
the longer one — see the *Length Is Not the Problem* write-up. The differentiator is orientation,
not length: a persistent anchor, related things adjacent, no recirculation mid-evaluation, and
real density.

### Measured evidence base

| at 375 × 812, fold = 741px | card under hero | persistent nav |
|---|---|---|
| Total price bottom | 832px | 708px |
| Whole page | 1.98 screens | 1.82 screens |

Path 1 one-scroll 2.00 screens vs layers 1.00. Path 2 longest turn 2.58 → 1.44 screens.

## Open questions

Tracked in `../mobile-guided-path-codex-handoff.md` and its coordination log. The live ones:

1. **Concept C has no Compare affordance on screens 1–3** — the Echo dock owns the bottom of the
   screen, so C4 is only reachable from the controls panel. The biggest open item.
2. Green vs dark primary action — moot while the build is greyscale, live again when colour
   returns.
3. Is "How does it compare?" the same destination as the Car Comparison control? They are today.
4. Comparison cap — 4, 5 or 6. The module says 4 throughout.
5. Should the collapsed and expanded decide control share one label? The geometry is now
   pixel-identical; the words are the only thing that still changes.
