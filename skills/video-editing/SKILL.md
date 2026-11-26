---
name: video-editing
description: Master creative director and professional video editing pipeline. Combines commercial creative direction, editorial rhythm and pacing, motion design craft (Disney's 12 principles, kinetic typography, frosted glassmorphism), surgical sound design (transient alignment, micro-trimming, EBU R128 mastering), and technical execution via HyperFrames and FFmpeg. Use whenever the user asks to create, edit, direct, pace, score, polish, or render any video, reel, short, promo, or explainer.
---

# 🎬 Master Video Editing & Creative Direction

This skill transforms the agent from a pure code generator into an **Executive Creative Director and Senior Film Editor**. Code (HTML/GSAP/FFmpeg) is strictly an invisible execution canvas; all decisions are governed by storytelling, visual rhythm, human pacing, typographic prestige, and emotional sound design.

---

## 🏛️ The Unified 9-Stage Hard-Gated Pipeline

Every video project—whether 15s Shorts, 30s Reels, or 2-minute product films—follows this single chronological pipeline, pausing for explicit user sign-off at every gate (`Gate 1` → `Gate 7`):

```mermaid
flowchart LR
    S1[Stage 1: Brief & 5-Track PLAN.md] -->|Gate 1| S2[Stage 2: UI Preview & Motion Craft]
    S2 -->|Gate 2| S3[Stage 3: Footage / CFR Prep]
    S3 -->|Gate 3| S4[Stage 4: VO & Timeline Timing Lock]
    S4 -->|Gate 4| S5[Stage 5: SFX Locked to Animation]
    S5 -->|Gate 5| S6[Stage 6: BGM Stem]
    S6 -->|Gate 6| S7[Stage 7-8: 5-Stem Mix & Cross-Device QA]
    S7 -->|Gate 7: 48kHz 24-bit WAV| S9[Stage 9: Render, Mux & Delivery QA]
```

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

*Detailed guides*: Read [references/creative-direction.md](references/creative-direction.md), [references/editorial-rhythm.md](references/editorial-rhythm.md), and [references/reference-2-0-styles.md](references/reference-2-0-styles.md).
**🛑 Gate 1**: Stop for user approval of `PLAN.md` (`Clips`, `Motion`, `VO`, `SFX`, `BGM`) before building UI or spending credits.

---

## Stage 2: Motion Design & Interactive UI Preview *(🛑 Gate 2 — Zero Render, Token-Saving Wireframe)*

Build `layout_preview_widget.html` + `contact_sheet.html` with zero AI visual slop **and zero wasted illustration tokens**:

0. **Time & Token-Saving Wireframe Rule (Mandatory)**:
   - For scenes driven by video/Flow footage, render **clean labeled wireframe boxes** displaying the clip name, slot role, and camera move (`[VIDEO: Flow 01 — Temple Grandeur · Z-Dolly In]`) rather than hand-coding multi-path fake SVG buildings, carvings, or human characters.
   - Spend Stage 2 layout fidelity on **real typography, exact brand palette, contrast scrims, safe-zone spacing, and transition choreography** — reserve real vector/SVG tracing for true Motion Graphics scenes using real reference frames (`Stage 3 / Stage 9`).

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
   - **Organic Foreground Overlays**: Use deterministic `f(time)` foreground sweeps matched to the reel's world (e.g., silhouette birds flying across frame for heritage/nature, drifting mist, doorway/pillar wipes), switching scenes under the peak visual pass alongside matched SFX.
   - **Cinematic Component Focus-Zoom**: Rack camera focus onto one key component (room card, carved detail, telemetry badge, or pin) via wrapper `transformOrigin` + GPU `scale` dive (`cinematic-zoom` / custom GSAP) straight into full-bleed spatial footage (`data-media-start`).
   - **VO-Synced Clips Inside Cards**: Keep card grids/split containers alive by scrubbing/playing muted motion clips *inside* cards synced to individual VO phrases (`Stage 4` `WordBoundary` cues) instead of static stills.

*Detailed guide*: Read [references/motion-design-craft.md](references/motion-design-craft.md).
**🛑 Gate 2**: Deliver interactive `layout_preview_widget.html` + `contact_sheet.html` and wait for UI & transition approval before sourcing paid footage or audio.

---

## Stage 3: Footage Sourcing & Closed-GOP CFR Media Prep *(🛑 Gate 3)*

Confirm staged clips vs. Google Flow generations (`flowmcp.md`). Transcode every clip to deterministic Closed-GOP CFR (`fps=30, -g 30 -keyint_min 30 -sc_threshold 0 -flags +cgop -fps_mode cfr -an`) and pre-prime `<video>` elements (`muted playsinline`, no duplicate `autoplay loop`).

---

## Stages 4–8: Independent Audio Production Pipeline *(Gated Stem-by-Stem)*

Never drop BGM and random SFX straight onto video timelines. Audio is planned (`Stage 1`), built and audited separately (`Stages 4–6`), mixed (`Stage 7`), cross-device tested (`Stage 8`), and approved as **`48 kHz · 24-bit PCM WAV`** before attaching to video:

1. **Stage 4 — Voice Agent (`VO` Only → 🛑 Gate 4)**:
   - Generate per-page WAVs (`48 kHz · 24-bit`, `<= +8%` rate, `boundary="WordBoundary"` + empty word-list guard), strip leading silence, audit WPM/headroom/tail gaps (`0.5s–1.4s`).
   - **Approved VO establishes final timing** — lock HTML/rough-cut transition & animation timestamps to actual VO duration before Stage 5!
2. **Stage 5 — Sound Designer (`SFX` & Foley Only → 🛑 Gate 5)**:
   - Place cues strictly against the **VO-locked animation preview or rough cut**, never guessed from script.
   - Pre-process with `0ms` attack latency, `10ms` micro-fades, `1.5s–3.0s` negative space (`<= 1.2s` active SFX per 30s), and active duration caps (clicks **40–120ms**, pops **60–180ms**, sweeps **180–380ms**, hits **250–400ms**). Audition isolated `sfx_only` stem at **-10 to -15 dBFS RMS**.
3. **Stage 6 — Music Agent (`BGM` Only → 🛑 Gate 6)**:
   - Prepare instrumental track (`highpass=85Hz, lowpass=8500Hz` speech carve), verify domain energy curve & frequency headroom, audition separately.
4. **Stage 7 — Audio Mixing Engineer (`5-Stem Mix` → `48 kHz · 24-bit WAV`)**:
   - Duck BGM smoothly (`0.095–0.14` under VO → `0.24–0.40` in breaks, `220ms` cosine ramps), apply `-2.5 dB / 70ms` vocal pockets over mid-dialogue transients, and run 2-pass linear EBU R128 normalization (**`-14.0 LUFS ± 0.5`**, **`LRA <= 7.0 LU`**, **`TP <= -1.0 dBTP`**).
5. **Stage 8 — Cross-Device QA & Independent Review *(🛑 Gate 7 — Approved Audio Master)***:
   - Test across **Mobile Mono (`250Hz–7kHz`, `-ac 1`) · Laptop · Headphones · Television · Full-Band Mono Fold-down**, verify zero masking/distortion/phase drop/timing drift, and wait for user approval of **`master_audio_ebur128.wav`** before Stage 9.

*Detailed guide*: Read [references/sound-design-mastery.md](references/sound-design-mastery.md) and `professional-sound-design/SKILL.md`.

---

## Stage 9: Headless Render, Audio Integration & Final Delivery QA *(🚀 Ship)*

Execute the render cleanly using HyperFrames and FFmpeg:

1. **Composition Architecture**:
   - Composition entry point: `index.html` (`1080×1920 @ 30fps` for vertical reels, `1920×1080` for widescreen), synced strictly to approved Stage 4–8 timestamps.
   - Ensure all `<video>` elements use `muted playsinline` without duplicate `autoplay loop` attributes, and mark non-reading HUD/watermark elements with `data-layout-ignore`.
2. **Verification Protocol**:
   - Run `hyperframes check` (`0` lint errors, `0` runtime errors, `0` collision issues, 100% WCAG AA contrast).
3. **Render, Fast Mux & Post-Export Audit**:
   - Headless render: `npx hyperframes render . -o raw_video.mp4 -q looks --format mp4`
   - Fast 0.5s mux: `ffmpeg -y -i raw_video.mp4 -i master_audio_ebur128.wav -map 0:v:0 -map 1:a:0 -c:v copy -c:a aac -b:a 320k -ar 48000 -shortest master_deliverable.mp4`
   - Final Delivered MP4 Audit: measure `ebur128=peak=true` (`-14.0 LUFS ± 0.5`, `TP <= -1.0 dBTP`), run `-af "highpass=f=250,lowpass=f=7000" -ac 1` mono mobile audition, listen/transcribe delivered speech + SFX hits, and inspect 6 extracted key-frame stills.

*Detailed guide*: Read [references/hyperframes-engine.md](references/hyperframes-engine.md) and field-tested guardrails in [references/production-lessons-reel03.md](references/production-lessons-reel03.md).
