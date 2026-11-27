---
name: dont-do-in-video-edit
description: Strict anti-pattern checklist and quality gate covering everything NOT to do in AI video editing, motion graphics, UI design, transitions, GSAP timelines, SFX/audio mixing, and rendering. Consult before building scenes, writing transitions, styling HUDs, slicing SFX, or delivering any final video.
---

# Don't Do in Video Edit (`dont-do-in-video-edit`)

Use the [general editing skill](../video-editing/SKILL.md) first. The rules below address specific failures in commercially animated reels. Apply each rule only to the corresponding creative choice, technology or audio track.

---

## 1. Generic PowerPoint & Slideshow Anti-Patterns
- **NO slide-deck layouts or cross-reel cloning**: Never center boxy rectangular cards with bullet lists on flat backgrounds, AND never lazily clone a previous reel's UI skeleton (same card layout, pill stepper, and closer halo) into a new domain. Choose depth, palette, and UI framing (full-bleed footage, unboxed editorial type, or intentional bento containers) fresh for each creative brief.
- For a moving shot, check continuity through the cut. Hold a frame steady when the viewer needs to read or listen.
- For match-on-action cuts, keep motion continuous across the edit.
- **NO generic filler slogans**: Never write copy that passes on any random company (*"Trusted Quality"`, `"Modern Solutions"`). Run the **Logo Test** (`pv-story`): prove specific proof points (`8K HDR`, `±1.2mm LiDAR`, `Google Blue-Line`).

---

## 2. PowerPoint / Slideshow Transition Mistakes
- **NO generic crossfades, box wipes, or linear slides**: Never cut between scenes using basic `opacity: 0 -> 1` dissolves, linear slides, or mismatched exit/entry axes (e.g., exiting left while next scene slides down). Choose motivated cuts—velocity camera moves, **component focus-zooms** (`transformOrigin` + GPU wrapper scale), or **deterministic motivated foreground/optical wipes** (e.g., depth sweeps, light curtains, or frame-edge wipes synced at occlusion peak, never `Math.random()` / CSS keyframes).
- **NO static dead cards during VO**: When narration lists multi-room/campus/facility features, avoid static text-only boxes—play pre-primed muted clips cleanly *inside* cards synced to `Stage 4` `WordBoundary` cues, and pass `data-media-start="<sec>"` on continuous PiP/focus-zoom docks (`never` reset video to `0.0s`).
- **NO card-to-scene sequence mismatch**: Preview card strips (`Card 1 -> Card 2 -> Card 3`) must **never** disagree with the actual scene walkthrough order.
- **NO empty transition voids or broken focus-zooms**: Never leave an empty dark background or flat placeholder polygon on screen for `>0.3s` during a transformation, and never zoom into an object only to hard-cut onto the back of a device or mismatched angle.
- **NO black-frame flashes**: Never leave a sub-composition timeline shorter than `data-duration` (`tl.duration() < data-duration`).

---

## 3. Glitch, Loop & Repeat Element Bugs
- **NO `1 -> 0 -> 1` flash on delayed `.fromTo(..., { immediateRender: false })` children**: Whenever a scene viewport fades in before staggered children animate, **always** `.set(...)` every delayed child's hidden starting state (`opacity: 0`, `yPercent`, `scale`, `scaleX/Y`) explicitly at `t = 0`. Never let incoming scenes jump to `opacity: 1` over an unfinished outgoing exit (`z-index` pop), never stack full-viewport `filter: blur()` over `backdrop-filter`, and always pre-prime `<video>` `currentTime` + debounce async `play()`.
- **NO `.add(() => updateDOM())` text mutations mid-transition**: Calling JS functions from GSAP `.add()` paired with partial opacity re-tweens (`opacity: 0.4 -> 1`) causes scrubbing glitches, stale text flashes, and double-popping cards. Stack pre-rendered static DOM slots and cross-fade them deterministically *after* whip-pans land.
- **NO duplicate/overlapping sheen or entrance tweens**: Never apply `addSheen()` 3 times on one persistent card or double-trigger card stagger animations.
- **NO non-transform GSAP animations**: Never animate `left`, `top`, `width`, `height`, or `letterSpacing` (triggers HyperFrames `gsap_non_transform_motion` lint errors and layout jitter). Animate pure GPU transforms (`x`, `y`, `xPercent`, `scale`, `rotateX/Y`, `opacity`, `backgroundColor`).
- **NO non-deterministic browser state**: Never use `Math.random()`, `Date.now()`, `setTimeout`, `requestAnimationFrame`, CSS `transition`, or GSAP `repeat: -1` inside deterministic timelines. Scrubbing and headless capture require pure `f(time)` timelines.

---

## 4. UI, Typography & Container Failures
- **NO hardcoded pixel widths/X-offsets on multi-step pills**: Never write `width: 117px; x: 236` on segmented sliders. Whenever render canvas (`412px`) and browser preview (`420px`) differ, pills overhang or leave asymmetric gaps (`03 · Confident` drift). **Always** use proportional CSS `width: calc((100% - <padding*2>) / <count>)` + GSAP **`xPercent: 0 -> 100 -> 200`**.
- **NO washed-out or cluttered UI plates**: Never drop low-contrast pills ungrounded over busy footage, and never trap every headline, stat, and video inside repetitive rounded glass boxes when clean edge-to-edge footage + soft `.scrim` + `1px` hairlines reads cleaner. Match surface style (plateless editorial vs. layered bento cards) to the brief.
- **NO Unicode emojis or italic slop**: Never stamp system emojis (`🏥`, `🎓`, `✅`, `🔥`) in commercial graphics; use inline monochrome/dual-tone Lucide SVGs. Choose brief-matched geometric display/UI/mono fonts, **zero unsolicited italics**.
- **NO clipped edge labels**: Keep labels safely inside `60px` outer margins; mask rising headlines with `overflow: hidden` containers (`.k-mask`), never naked unbounded text scaling across viewport edges.

---

## 5. SFX & Audio Engineering Failures
- **NO blind fixed-offset slicing**: Never slice risers or cinematic whooshes using arbitrary numbers like `start_offset_s=0.15` or `5.8s` without first probing `np.argmax` (buildups can peak `2.5s–4.0s` inside a clip). Slice windows anchored around the **true acoustic crest** so impacts align frame-accurately.
- **NO `-22 dBFS` vanishing UI clicks**: Leaving short `50–120ms` taps/pops weak next to `-9 dBFS` bass slams makes them vanish on laptop/phone speakers unless the user cranks max volume. Normalize every individual SFX stem to **`-10 to -15 dBFS` RMS** (`-1.0 dBFS` peak) with crisp mid-range tactile body (`700–3500 Hz`).
- **NO untrimmed leading dead air**: Never drop raw SFX clips with 50–500ms silent intros onto frame 0 (`t_onset` lags behind the cut).
- **NO muddy continuous wall-of-sound or dialogue clashing**: Leave `1.5s–3.0s` negative space for voiceover breathing, organize stems cleanly (`01_page_transitions/`, `02_motion_elements_and_graphics/`, `03_animations/`), carve BGM (`highpass=85Hz, lowpass=8500Hz`, ducked `0.085–0.12` under speech), and apply `-2.5 dB / 70ms` vocal pockets when sharp foley hits mid-dialogue.
- **NO `+0.5 dBFS` true-peak clipping or broken phone audit**: Never trust non-oversampled limiters alone before MP3/AAC encoding, and never pass `ac=1` inside `-af`. Verify **`ffmpeg -i master_deliverable.mp4 -af ebur128=peak=true -f null -`** (`-14.0 LUFS ±0.5`, **`TP <= -1.0 dBTP`**) AND audition **`-af "highpass=f=250,lowpass=f=7000" -ac 1`** plus actual speech/SFX cues on the delivered MP4.
- **NO >+8% TTS speed-up squeezing**: Keep TTS speed `<= +8%` target (`+10%` hard max only if trimming copy is impossible) and trim filler words to obey `<= 2.2 words/sec` with `0.5s–1.4s` tail silence; flag any empty `WordBoundary` list immediately.
- **NO unapproved or untested audio integration**: Never auto-jump past audio gates or attach raw mixes straight to video. Build & approve **`VO` (`Stage 4`) -> `SFX` locked to actual VO-timed animation/rough-cut (`Stage 5`) -> `BGM` (`Stage 6`) -> 5-Stem Mix (`Stage 7`) -> 5-Profile Cross-Device QA (`Mobile`, `Laptop`, `Headphones`, `TV`, `Mono`) & Independent Review (`Stage 8`) -> `48 kHz · 24-bit WAV` Master** before muxing (`Stage 9`).

---

## 6. Hard-Gated Workflow & Verification Mistakes (`Stages 1–9`)
- For a preview use available footage and plain timed labels for missing assets. Reuse one player or a proxy export. Reserve custom illustrations and controls for an explicit deliverable.
- Obtain the required approvals for the agreed production stages. Carry earlier approvals forward and wait at the playable preview before polishing a creative cut.
- **NO SFX timed from script guesses**: Always let **Stage 4 VO** establish real spoken durations & `WordBoundary` anchors first, snap UI animation/rough-cut cut frames to that VO, and only then lock **Stage 5 SFX** onto actual visual frame timestamps.
- **NO stale verification screenshots on Windows**: Chrome headless `--screenshot` silently fails or hits locks on paths with spaces or default user profiles. Always write to a space-free scratch path with an isolated `--user-data-dir` + `Start-Process -Wait`, then copy cleanly.
- **NO unverified delivery**: Never mark a render done without running `hyperframes check`, `ffprobe` stream inspection, `ebur128=peak=true` loudness check, 5-profile cross-device audio check, actual delivered MP4 VO/SFX audition, and visual `read_file` verification of **post-edit** extracted video strips.
