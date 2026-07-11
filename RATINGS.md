# presets/video — review ratings

Working notes for reviewing the video-reactive presets. A "sub-preset" is a distinct
look produced by one `.milk` file (e.g. `flipbook.milk` picks one of five artistic
filters per run via `rand_preset`); each is rated on its own, since they succeed or
fail independently.

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
| blob-shadow — various artists | — | |
| falling — Hexcollie, Spooky nz+ psychos on the internet | — | In the top-level `favorites.txt`. |
| ghost — Geiss, Skin Dots 10b (video motion reaction) | — | |
| ghost color zoom — Geiss, Skin Dots 10b | — | |
| ink-shadow — various artists | — | |
| recursive quad — time-offset | — | |
| rorschach — suksma, broadcloak flacc roam3 nz+ | — | In the top-level `favorites.txt`. |
| rorschach x 3 — suksma, broadcloak flacc roam3 nz+ | — | |
| splitscan — Flexi + geiss, the deep diver's manifesto | — | |
| suksma — biotoxins on strings, walk on it | — | In the top-level `favorites.txt`. |
