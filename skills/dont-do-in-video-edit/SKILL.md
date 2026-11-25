---
name: dont-do-in-video-edit
description: Strict anti-pattern checklist and quality gate covering everything NOT to do in AI video editing, motion graphics, UI design, transitions, GSAP timelines, SFX/audio mixing, and rendering. Consult before building scenes, writing transitions, styling HUDs, slicing SFX, or delivering any final video.
---

# Don't Do in Video Edit (`dont-do-in-video-edit`)

A permanent blacklist of visual, editorial, motion, UI, GSAP, SFX, and render mistakes caught in real production reels. **Never ship a video that triggers any rule below.**

---

## 1. Generic PowerPoint & Slideshow Anti-Patterns
- **NO slide-deck layouts**: Never center boxy rectangular cards with bullet lists on pale flat backgrounds, separated by blank fades. Build layered spatial depth (`~50%` footage + `~50%` glassmorphic HUD/bento graphics over dark aurora obsidian `#070B15` grounds).
- **NO dead still frames**: Never freeze the camera completely for `> 2.0s` (`MOTION_PHILOSOPHY` Law #4: *"Camera never sleeps"*). Keep continuous subtle scale push-ins, parallax, or orb drift alive.
- **NO stop-then-cut timing**: Never let motion come to a dead halt *before* switching scenes. Cuts must ride active acceleration (`velocity-matched cuts`).
- **NO generic filler slogans**: Never write copy that passes on any random company (*"Trusted Quality"`, `"Modern Solutions"`). Run the **Logo Test** (`pv-story`): prove specific proof points (`8K HDR`, `±1.2mm LiDAR`, `Google Blue-Line`).

---

## 2. PowerPoint / Slideshow Transition Mistakes
- **NO generic crossfades, box wipes, or linear slides**: Never cut between scenes using basic `opacity: 0 -> 1` dissolves, linear slides, or mismatched exit/entry axes (e.g., exiting left while next scene slides down).
- **NO jarring clip restarts on PiP docks**: When Scene N docks into a mini card in Scene N+1, **never** let the video reset to `0.0s`. Pass `data-media-start="<sec>"` cleanly in HTML and preview playback.
- **NO card-to-scene sequence mismatch**: Preview card strips (`Card 1 -> Card 2 -> Card 3`) must **never** disagree with the actual scene walkthrough order.
- **NO black-frame flashes**: Never leave a sub-composition timeline shorter than `data-duration` (`tl.duration() < data-duration`).

---

## 3. Glitch, Loop & Repeat Element Bugs
- **NO `.add(() => updateDOM())` text mutations mid-transition**: Calling JS functions from GSAP `.add()` paired with partial opacity re-tweens (`opacity: 0.4 -> 1`) causes scrubbing glitches, stale text flashes, and double-popping cards. Stack pre-rendered static DOM slots and cross-fade them deterministically *after* whip-pans land.
- **NO duplicate/overlapping sheen or entrance tweens**: Never apply `addSheen()` 3 times on one persistent card or double-trigger card stagger animations.
- **NO non-transform GSAP animations**: Never animate `left`, `top`, `width`, `height`, or `letterSpacing` (triggers HyperFrames `gsap_non_transform_motion` lint errors and layout jitter). Animate pure GPU transforms (`x`, `y`, `xPercent`, `scale`, `rotateX/Y`, `opacity`, `backgroundColor`).
- **NO non-deterministic browser state**: Never use `Math.random()`, `Date.now()`, `setTimeout`, `requestAnimationFrame`, CSS `transition`, or GSAP `repeat: -1` inside deterministic timelines. Scrubbing and headless capture require pure `f(time)` timelines.

---

## 4. UI, Typography & Container Failures
- **NO hardcoded pixel widths/X-offsets on multi-step pills**: Never write `width: 117px; x: 236` on segmented sliders. Whenever render canvas (`412px`) and browser preview (`420px`) differ, pills overhang or leave asymmetric gaps (`03 · Confident` drift). **Always** use proportional CSS `width: calc((100% - <padding*2>) / <count>)` + GSAP **`xPercent: 0 -> 100 -> 200`**.
- **NO washed-out pale UI on raw video**: Avoid flat translucent white pills floating ungrounded on full-bleed footage. Wrap featured footage in explicit rounded glass-bordered containers (`#s05-video-frame` + live badge) paired with dark multi-stop frosted bento cards (`rgba(..., 0.90)` + top `1px` specular catchlight).
- **NO Unicode emojis or italic slop**: Never stamp system emojis (`🏥`, `🎓`, `✅`, `🔥`) in commercial graphics; use inline monochrome/dual-tone Lucide SVGs inside glass badges. Stick strictly to approved geometric fonts (`Google Sans` + `Satoshi`), **zero italics**.
- **NO clipped edge labels**: Keep labels safely inside `60px` outer margins; mask rising headlines with `overflow: hidden` containers (`.k-mask`), never naked unbounded text scaling across viewport edges.

---

## 5. SFX & Audio Engineering Failures
- **NO blind fixed-offset slicing**: Never slice risers or cinematic whooshes using arbitrary numbers like `start_offset_s=0.15` or `5.8s` without first probing `np.argmax` (buildups can peak `2.5s–4.0s` inside a clip). Slice windows anchored around the **true acoustic crest** so impacts align frame-accurately.
- **NO `-22 dBFS` vanishing UI clicks**: Leaving short `50–120ms` taps/pops weak next to `-9 dBFS` bass slams makes them vanish on laptop/phone speakers unless the user cranks max volume. Normalize every individual SFX stem to **`-10 to -15 dBFS` RMS** (`-1.0 dBFS` peak) with crisp mid-range tactile body (`700–3500 Hz`).
- **NO untrimmed leading dead air**: Never drop raw SFX clips with 50–500ms silent intros onto frame 0 (`t_onset` lags behind the cut).
- **NO muddy continuous wall-of-sound or dialogue clashing**: Leave `1.5s–3.0s` negative space for voiceover breathing, organize stems cleanly (`01_page_transitions/`, `02_motion_elements_and_graphics/`, `03_animations/`), carve BGM (`highpass=85Hz, lowpass=8500Hz`, ducked `0.085–0.12` under speech), and apply `-2.5 dB / 70ms` vocal pockets when sharp foley hits mid-dialogue.
- **NO `+0.5 dBFS` true-peak clipping**: Never trust non-oversampled limiters alone before MP3/AAC encoding. Always verify `ffmpeg -af ebur128=peak=true` and enforce **`-14.0 LUFS (±0.5)`** + **`TP <= -1.0 dBTP`**.
- **NO >+11% TTS speed-up squeezing**: Never crank voiceover rates up to force bloated copy into 30s—trim filler words to obey `<= 2.2 words/sec` with `0.5s–1.4s` tail silence.

---

## 6. Workflow & Verification Mistakes
- **NO rendering 900 frames before UI/timing lock**: Follow *Preview-First, Render-Last* (`PLAN.md` → layout preview widget + `contact_sheet.html` → isolated VO & SFX audition → MP4 render → fast `-c:v copy` mux).
- **NO stale verification screenshots on Windows**: Chrome headless `--screenshot` silently fails or hits locks on paths with spaces or default user profiles. Always write to a space-free scratch path with an isolated `--user-data-dir` + `Start-Process -Wait`, then copy cleanly.
- **NO unverified delivery**: Never mark a render done without running `hyperframes check`, `ffprobe` stream inspection, `ebur128` loudness check, and visual `read_file` verification of **post-edit** extracted video strips.
