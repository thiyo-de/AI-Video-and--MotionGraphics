# Production Lessons Learned — Project 3 (`ruthram360-hospital-reel03`)

Battle-tested rules extracted from building, debugging, and mastering Reel 03 across HyperFrames, GSAP, Chrome previewing, SFX design, and EBU R128 final assembly. Apply these defaults on all upcoming reels.

---

## 1. Video Continuity & Scene Matching
- **Seamless Cross-Scene Clip Continuation**: When a hero shot carries from Scene N into a picture-in-picture card in Scene N+1, carry forward the outgoing timestamp via `data-media-start="<sec>"` in `index.html` and `mediaStart` inside `layout_preview_widget.html`'s `videoClips` / `syncVideos()` so playback does not reset to `0.0s`.
- **Card Order = Scene Order**: Always keep preview thumbnails (e.g. `STERILE OT → ICU WARD → SUITES`) in the exact chronological sequence they appear in the following showcase scene, and trigger the zoom transition from the matching first card (`#s02-t1`).

## 2. Glitch-Free GSAP & HyperFrames Compliance
- **Zero `.add()` Text Mutations Inside Transitions**: Never swap HUD labels or card copy with GSAP `.add(() => fn())` callbacks during whip-pans or wipes; scrubbing and non-linear frame capture cause desynced flashes or double-pops. Instead, stack pre-rendered static DOM slots inside the container and cross-fade them deterministically *after* the whip-pan lands (`opacity` + small `y` translate).
- **Transform-Only Tweens**: Animate strictly GPU transforms (`x`, `y`, `xPercent`, `scale`, `rotateX/Y`, `opacity`, `backgroundColor`). Avoid tweening `letterSpacing` or `left`, which fail HyperFrames `gsap_non_transform_motion` lint rules.
- **Relative Stepper Pill Sizing (`0px` Drift Across Viewports)**: Never hardcode pixel widths and `x` offsets (`117px` + `x: 236`) on segmented pill sliders—canvas widths frequently differ between render (`412px`) and browser preview (`420px`). Use `width: calc((100% - <padding*2>) / <tabs>);` and tween `xPercent: 0 → 100 → 200` so left/right margins and label centering stay flush on every viewport.

## 3. Dark Gradient Bento & Framed Footage Craft
- Avoid pale/low-contrast white cards stamped directly on raw full-bleed footage when multi-card telemetry needs hierarchy.
- Wrap live video in an explicit rounded glass-bordered container (`#s05-video-frame` with bottom telemetry badge) above/below a dark multi-stop frosted gradient bento card (`#s05-ar`, `#s06-stage`) over a dark aurora background.

## 4. Surgical Peak-Anchored SFX & Mobile Audibility
- **Peak-Anchor Every Sweep**: Never slice transition whooshes or risers at hardcoded millisecond offsets without measuring `np.argmax` first (source risers/whooshes often peak `2–4s` into the file). Extract windows centered around the acoustic crest so the transient lands cleanly on frame 0 of the transition.
- **Avoid `-23 dBFS` Inaudible UI Ticks**: Short `50–120ms` UI taps and gyro clicks vanish on laptop/phone speakers when raw-mixed beneath sub-bass slams. Bring individual UI/animation stems to **-10 to -15 dBFS RMS** (`-1.0 dBFS` peak), compress lightly + true-peak limit (`<= -1.0 dBTP`), and categorize stems separately (`01_page_transitions/`, `02_motion_elements_and_graphics/`, `03_animations/`) alongside full-timeline audition mixes (`sfx_only.mp3` / `.wav`).
- **Enforce True-Peak Headroom Before MP3 Encoding**: Always check final WAV/MP3 outputs with `ffmpeg -af ebur128=peak=true`. Non-oversampled limiters can overshoot `+0.5 dBFS` on encode; target `TP <= -1.0 dBTP` via two-pass linear `loudnorm`.

## 5. Windows Render & Verification Discipline
- **Isolated Chrome `--screenshot`**: On Windows, Chrome headless `--screenshot` can silently skip writing or hit locks if the path has spaces or shares a profile. Always pass a space-free output path plus an isolated `--user-data-dir` and `Start-Process -Wait`, then copy to the project directory.
- **Verify Post-Edit Outputs Empirically**: Inspect extracted FFmpeg verification strips across key transitions/steps, confirm stream counts with `ffprobe`, and measure loudness (`ebur128`) after every final edit.
