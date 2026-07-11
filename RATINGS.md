# presets/video — review ratings

Working notes for reviewing the video-reactive presets. A "sub-preset" is a distinct
look produced by one `.milk` file (e.g. `flipbook.milk` picks one of five artistic
filters per run via `rand_preset`); each is rated on its own, since they succeed or
fail independently.

## How to review (two ways to fool yourself)

Both of these silently produced wrong verdicts during this review:

1. **Review with music playing, and check the mic actually opened.** A preset name that matches no
   device does not error — it falls back to the system default, which here is silence. Look for
   `Selected audio device '...'` in the log. Deaf, audio-reactive presets look dead or static, and
   several were nearly deleted on that basis.
2. **Look at the COMPOSITE, not the pre-composite drawing.** The composite shader can crop, curve,
   shade and frame the image, so the two can look like different presets. Capture with
   `PROJECTM_SCREENSHOT_SURFACE=comp` (what the viewer sees) — `main` is the warp output, useful
   when debugging the drawing itself, misleading when judging the look.
3. **Stills systematically undersell motion.** Anything whose appeal is temporal — slit-scan,
   feedback trails, page-flips — looks worse frozen than it is. `splitscan` reads as an illegible
   smear in a still and is superb in motion. Watch it live before rating it down.

## Scale

| Stars | Meaning |
|---|---|
| ★★★★★ | Excellent. Ship it; a highlight of the set. |
| ★★★★ | Probably done. Good enough to add to the appliance. |
| ★★★ | Promising, but needs specific work before it ships. |
| ★★ | Rough. The idea reads, the execution doesn't. |
| ★ | Not working. Rethink or drop. |
| — | Not reviewed yet. |

## flipbook.milk

Live video stylised as a flipbook on a desk; one filter is chosen per run.
Pin a filter for review by hardcoding `filt_` (see the comment at the `filt_`
declaration in the warp shader).

| # | Sub-preset | Rating | Notes |
|---|---|---|---|
| 0 | Flipbook — Kuwahara (watercolor) | ★★★★ | Keeper. Kuwahara flatten + posterized paint bands, subject popped off whitened paper. Fine ink lines added: paint-band boundaries (subject only) + seg-mask silhouette, both suppressed in already-dark paint so the lines don't muddy the shadows. |
| 1 | Flipbook — charcoal | — | Sobel strokes + tonal shading + paper grain on warm paper. Reverted to the committed version: attempts to improve it kept drifting toward *pencil*, and the mass-based rework that resulted became filter 5 instead. If revisited, the honest charcoal direction is mass-not-line (see filter 5), not lighter lines. |
| 2 | Flipbook — line drawing | — | Multi-scale Sobel contours + posterized ink wash on the subject. |
| 3 | Flipbook — comic book | — | CMYK-quantised cels + Ben-Day halftone + ink; desaturated background. |
| 4 | Flipbook — take on me | — | Pencil rotoscope; contours + loose scribble shading, boils per page. |
| 5 | Flipbook — Harold (purple marker) | ★★★★ | Keeper. **Two inks**, as in the book: the *world* is drawn in purple marker `#9a1482` (sampled from the art) — sparse, solid, continuous lines on bare paper, boiling per page like redrawn animation; the *subject* is black line over flat posterized colour cels (Harold himself is black-line in the book). Interior lines are sparing (the cels do that work); the silhouette comes from the seg mask so the figure holds against the world even at matching tones. Uses the new `warp_pre_` pass for its pre-blurred luminance. |

## Other presets

| Preset | Rating | Notes |
|---|---|---|
| rorschach — suksma, broadcloak flacc roam3 nz+ | ★★★★★ | The best of the set. Mirrored figure emerging from an ink blot; the dark field is what makes the symmetry read as a Rorschach rather than a kaleidoscope. Its `video_` shader (motion-gated seg matte) only started running once the palette-sampler bug was fixed — it is richer now than in any earlier capture. Cleaned up: 76 dead lines removed (all four disabled `wavecode_*` blocks + disabled `shapecode_3`; shapes 0–2 are live and draw the figure). Absorbed the identical `rorschach x 3` (same code, plus a commented-out film-negative experiment). |
| blob-shadow — various artists | ★★★ | Glowing green figure against a blue blob field. Reads clearly in the composite (it looked far weaker in the pre-composite view, which is what the broken screenshot was showing). |
| falling — Hexcollie, Spooky nz+ psychos on the internet | ★★★★ | Good for what it is. |
| ghost — Geiss, Skin Dots 10b (video motion reaction) | — | Shimmering moiré ripple field, figure dissolving through it. Only 5 lines from `ghost color zoom`. **Needs audio to judge** — it looks dead in silence. |
| ghost color zoom — Geiss, Skin Dots 10b | — | As above but louder: bigger colour blooms, stronger zoom. |
| splitscan — Flexi + geiss, the deep diver's manifesto | ★★★★★ | Slit-scan / time-smear: vertical strips sampled from different points in the video history, so motion drags into flowing ribbons; hot reds/oranges against acid green, with hard vertical banding snapping in on transients. **The figure is barely legible** — a person-shaped disturbance rather than a subject — and in stills that looks like a flaw. It isn't: in motion this is one of the best things in the set. Cleaned up: 222 dead lines removed (489 → 267; all 8 wave/shape blocks disabled, plus their code bodies). |
| recursive quad — time-offset | — | |
| suksma — biotoxins on strings, walk on it | — | |
