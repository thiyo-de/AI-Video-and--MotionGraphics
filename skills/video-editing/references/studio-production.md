# Studio production guide

Use these recipes for the approved stages of a commissioned motion and sound production. Visual styles, pacing and audio numbers below are examples for this studio format. Use the project brief for each choice.

For the canonical 9-stage gated pipeline (`PLAN.md` → rough cut → CFR → `VO → SFX → BGM → WAV Master` → `0.5s` render/mux), see `video-workflow.md` in the framework root. Confirm applicable gates with the user and follow stages below in order.

---

## Stage 1: Creative Direction, Hook & 5-Track `PLAN.md` *(🛑 Gate 1)*

Before writing any timeline or composition code, establish the commercial intention and run `/planning-video`:

1. **The Core Emotional Contrast**:
   - Every high-converting video contrasts an old painful reality with a new effortless reality.
   - *Example (Ruthram360)*: Frustrating, flat 20-page PDF brochure (Dull / Ignored) vs 8K HDR Interactive Spatial Twin (Exciting / Instant Trust).
2. **The 3-Second Hook Rule**:
   - The first 1.2 to 2.5 seconds must contain a visual pattern interrupt. Never start with a generic logo splash or slow fade-in.
   - Hook techniques: Bold controversial question, physical rejection stamp, extreme macro zoom, or rapid split-screen comparison.
3. **Target Audience & Tone**:
   - B2B / Enterprise (Chancellors, Directors): Calm, authoritative, prestigious, spacious.
   - Consumer / Tech SaaS (Linear/Stripe style): Hyper-sleek, snappy, dark obsidian, neon micro-accents.
   - Social / Viral: High-energy beat-synced, punchy kinetic type, rapid curiosity loops.
4. **Script Speaking Rate Golden Rule (Budgeted in `Stage 1`, Executed in `Stage 4`)**:
   - Natural human conversational speech is **130 to 145 Words Per Minute (WPM)** (≈ 2.2 words/second).
   - In a 30.0-second commercial reel: 0.5s visual hook + 2.5s–3.5s musical outro = **Net speech window ~26.0s (50–54 words max)**.
   - **Strict Prohibition**: NEVER speed up TTS beyond `+8%` target (`+10%` hard max). If voiceover exceeds the window, **edit the copy**.
   - **Action match cuts**: Plan J-cuts, L-cuts, and velocity-matched motion vectors (`1.0s–1.8s` hold for titles; `2.5s–4.0s` hold for spatial rooms).

*Detailed guides*: Read [references/creative-direction.md](creative-direction.md), [references/editorial-rhythm.md](editorial-rhythm.md), and [references/reference-2-0-styles.md](reference-2-0-styles.md).
**🛑 Gate 1**: Stop for user approval of `PLAN.md` (`Clips`, `Motion`, `VO`, `SFX`, `BGM`) before building UI or spending credits.

---

## Stage 2. Playable rough cut

Follow the preview instructions in the [general editing skill](../SKILL.md). Reuse existing footage, the timeline player or one draft MP4. Use simple labels for missing shots. Include the intended layout, motion, transitions and draft voice, effects and ambience. Mute background music during rough-cut review.

### Styling after preview approval

The following techniques are options for a brief that calls for designed graphics. Apply them during production.

1. **Zero System Emojis**:
   - ❌ **Forbidden**: Raw Unicode/Segoe UI emojis (`🏛️`, `🔬`, `📚`, `📲`, `❌`, `🎓`). They look cartoonish and cheap.
   - ✅ **Required**: Inline vector SVGs (Lucide / Feather style with `stroke-width: 1.75px` to `2.0px`) embedded in frosted glass micro-badge containers.
2. **Brief-Matched Typography Hierarchy** *(adapt font family to the brand; zero italic slop)*:
   - **Headlines / Punchwords**: Bold display grotesk (e.g., `Satoshi 900`, `Space Grotesk`, or architectural sans), uppercase, tight negative tracking.
   - **Body / Feature Labels**: Clean neutral geometric sans (`Google Sans 500/700`, `Inter`), comfortable line-height.
   - **Micro-Badges / Technical Readouts**: Tracked uppercase labels or monospace (`JetBrains Mono` / `Space Mono`, `tabular-nums`).
3. **Intentional Surface System (Plateless Type vs. Layered Cards — Choose One per Brief)**:
   - Let **real/Flow architectural footage breathe** using unboxed *"type without plates"* over subtle gradient scrims (`.scrim`) when visuals carry the space, OR choose multi-stop frosted cards where UI/HUD explanation demands structure (never box every headline/metric out of habit):
     ```css
     background: rgba(15, 23, 42, 0.65);
     backdrop-filter: blur(24px) saturate(180%);
     border: 1px solid rgba(255, 255, 255, 0.12);
     box-shadow: 0 20px 50px -10px rgba(0, 0, 0, 0.7);
     border-radius: 24px;
     ```
4. **Disney's 12 Animation Principles**:
   - **Anticipation**: Pull back 5% before launching forward.
   - **Overshoot & Settling**: Use spring physics (`power3.out` or custom cubic-bezier `0.22, 1, 0.36, 1`) rather than linear slides.
   - **Secondary Motion**: Badges follow cards with a 0.08s stagger delay.
5. **Creative Transitions & VO-Synced In-Card Clips**:
   - **Motivated Foreground & Optical Wipes**: Use deterministic `f(time)` foreground passes, depth-of-field sweeps, frame-edge wipes, or directional light curtains tailored to the project's aesthetic, switching scenes under the peak visual pass alongside matched SFX.
   - **Cinematic Component Focus-Zoom**: Rack camera focus onto one key component (room card, carved detail, telemetry badge, or pin) via wrapper `transformOrigin` + GPU `scale` dive (`cinematic-zoom` / custom GSAP) straight into full-bleed spatial footage (`data-media-start`).
   - **VO-Synced Clips Inside Cards**: Keep card grids/split containers alive by scrubbing/playing muted motion clips *inside* cards synced to individual VO phrases (`Stage 4` `WordBoundary` cues) instead of static stills.

*Detailed guide*: Read [references/motion-design-craft.md](motion-design-craft.md).
**Gate 2**. Obtain approval of the playable cut before producing finished visuals or spending on footage or audio.

---

## Stage 3: Footage Sourcing & Closed-GOP CFR Media Prep *(🛑 Gate 3)*

Confirm staged clips vs. Google Flow generations (`flowmcp.md`). Download raw footage strictly inside `projects/<project-name>/assets/raw/`, transcode every clip to deterministic Closed-GOP CFR in `assets/clips/` (`fps=30, -g 30 -keyint_min 30 -sc_threshold 0 -flags +cgop -fps_mode cfr -an`), and pre-prime `<video>` elements (`muted playsinline`, no duplicate `autoplay loop`).

---

## Stages 4–8: Independent Audio Pipeline *(🛑 Gates 4–7)*

Follow [professional-sound-design/SKILL.md](../../professional-sound-design/SKILL.md) and [sound-design-mastery.md](sound-design-mastery.md) for the full gated workflow (`VO` locks animation timings → pre-slice filtered `SFX` tucked `-2 to -6 dB` below VO → carved `BGM` → `-14.0 LUFS / <= -1.0 dBTP` `48 kHz · 24-bit WAV` master → 5-device QA with `highpass=f=350,lowpass=f=7000` mono check before Stage 9).

---

## Stage 9: Headless Render, Audio Integration & Final Delivery QA *(🚀 Ship)*

Execute the render cleanly using HyperFrames and FFmpeg:

1. **Composition Architecture**:
   - Composition entry point: `index.html` (`1080×1920 @ 30fps` for vertical reels, `1920×1080` for widescreen), synced strictly to approved Stage 4–8 timestamps.
   - Ensure all `<video>` elements use `muted playsinline` without duplicate `autoplay loop` attributes, and mark non-reading HUD/watermark elements with `data-layout-ignore`.
2. **Verification Protocol**:
   - Run `hyperframes check` (`0` lint errors, `0` runtime errors, `0` collision issues, 100% WCAG AA contrast).
3. **Render, Fast Mux & Post-Export Audit** *(all outputs inside `projects/<project-name>/export/`)*:
   - Headless render: `npx hyperframes render . -o export/raw_video.mp4 -q looks --format mp4`
   - Fast 0.5s mux: `ffmpeg -y -i export/raw_video.mp4 -i audio/master_audio_ebur128.wav -map 0:v:0 -map 1:a:0 -c:v copy -c:a aac -b:a 320k -ar 48000 -movflags +faststart -shortest export/master_deliverable.mp4`
   - Final Delivered MP4 Audit: measure `ebur128=peak=true` (`-14.0 LUFS ± 0.5`, `TP <= -1.0 dBTP`), run `-af "highpass=f=350,lowpass=f=7000" -ac 1` mono mobile audition, listen/transcribe delivered speech + SFX hits, and inspect 6 extracted key-frame stills. For a decoupled video-only deliverable without re-rendering, strip audio losslessly (`-map 0:v:0 -c:v copy -an -movflags +faststart`) into `video only/`.

*Detailed guide*: Read [references/hyperframes-engine.md](hyperframes-engine.md) and field-tested guardrails in [references/production-lessons-reel03.md](production-lessons-reel03.md).
