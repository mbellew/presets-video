# presets-video

MilkDrop presets that use a **live video input** as a texture source, for use with
[projectM](https://github.com/projectM-visualizer/projectM).

These presets read the camera/video feed through projectM's video-texture extension
(`GetVideo(uv, age)`, the `video_alpha_*` controls, and a foreground mask in the alpha
channel) and react to motion and to a segmented foreground figure.

## Presets

- **ghost - Geiss - Skin Dots 10b - video motion reaction** — Geiss "Skin Dots" reworked to
  react to video motion.
- **rorschach - suksma - broadcloak flacc roam3 nz+ - video** — a suksma preset driven by the
  video feed with a mirrored, ink-blot treatment.

## Requirements

A build of projectM with the video-texture feature, a configured video source
(`projectm_video_configure`), and `MILKDROP_PRESET_VERSION >= 200` with the
`PSVERSION_*` keys set so the warp/comp shaders load.
