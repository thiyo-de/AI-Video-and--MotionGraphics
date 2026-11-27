# ⚡ Studio Video Production Workflow (SOP)

Start with the [general video editing skill](skills/video-editing/SKILL.md). This SOP describes the full studio motion-production route. Agree on the tracks and gates for the brief before using the specialist recipes below.

> **Standard Operating Procedure for Fast, Error-Free AI Video Creation**  
> **Complements**: [ai-video-editing.md](ai-video-editing.md)
> **Core Philosophy**: **Preview-First, Render-Last.** Zero wasted render cycles.  
> **Governing Architecture**: **Strictly Page-by-Page (Screen-by-Screen).** Every single production asset, layout, voiceover line, and sound effect is authored and reviewed as an atomic page before whole-timeline assembly.  

---

> [!IMPORTANT]
> ## 🛡️ The Fundamental Law: Everything is Page-by-Page
> A video is **never** authored or processed as an uncontrollable 30-second or 60-second monolithic block.  
> A high-end video is an assembly of discrete, atomic **Pages (Screens)**.  
>
> **Every single Page is an independent creative unit** with 6 fixed parameters:
> 1. **Timecode & Duration Window**: Exactly defined start and end seconds (e.g. Page 1: `0.0s – 5.0s`, Page 2: `5.0s – 11.0s`).
> 2. **DOM Viewport Container**: Independent wrapper (`<div id="page-01-viewport">`) preventing transform bleed.
> 3. **Brief-Driven Layout & Motion**: Intentional visual craft (unboxed type over soft scrims OR frosted bento cards), metric counters, Lucide vector icons, and kinetic typography.
> 4. **Assigned Media Asset**: Specific CFR-transcoded video clip or static graphic mapped to that page.
> 5. **Dedicated Voiceover Sentence**: Word-budgeted narration line (strictly $\le 2.2\text{ words/sec}$, `<= +8%` rate) with breathing silence.
> 6. **Tailored SFX & Foley Cues**: Transition sweep entering the page, tactile foley locked to animation hits, and exit cues.
>
> **Never skip a gate. UI, Voiceover, SFX, Music, Cross-Device Audio Master, and Video Render each pause for explicit user approval.**

---

## The Unified 9-Stage Hard-Gated Pipeline

```
[Stage 1: Brief, Page Blueprint & 5-Track PLAN.md] ────────► 🛑 GATE 1: Plan & Audio Architecture Approval
                 │
[Stage 2: One playable rough cut] ─────────► 🛑 GATE 2: Rough Cut Approval
                 │
[Stage 3: Footage Sourcing, Clip Map & Closed-GOP CFR] ────► 🛑 GATE 3: Footage / Flow Spend Approval
                 │
 ┌───────────────┴────────────── INDEPENDENT AUDIO PRODUCTION PIPELINE ──────────────────────────────┐
 │ [Stage 4: Voice Agent — Isolated VO + WordBoundary + Lock Animation Cut Times] ──► 🛑 GATE 4: VO  │
 │               │                                                                                   │
 │ [Stage 5: Sound Designer — Isolated 3-Bucket SFX Locked to Real Animation] ──────► 🛑 GATE 5: SFX │
 │               │                                                                                   │
 │ [Stage 6: Music Agent — Isolated BGM Track & Speech Carve] ──────────────────────► 🛑 GATE 6: BGM │
 │               │                                                                                   │
 │ [Stage 7: Mixing Engineer — 5-Stem Bus & EBU R128 48 kHz · 24-bit WAV Master]                     │
 │               │                                                                                   │
 │ [Stage 8: 5-Device Cross-Device QA (Mobile/Laptop/Headphones/TV/Mono) + Review] ► 🛑 GATE 7: WAV │
 └───────────────────────────────────────────────────────────────────────────────────────────────────┘
                 │
[Stage 9: HyperFrames Render (-q looks), 0.5s Audio Mux & Final MP4 QA] ────────────► 🚀 DELIVER & SHIP
```

---

## Stage 1: Page-by-Page Blueprint, Media Classification & `PLAN.md` *(🛑 Gate 1)*

**Goal**: Partition the total video runtime into discrete Pages (Screens), classify footage/motion per page, and draft the **Master Audio Director Plan** inside `PLAN.md` before spending credits, recording audio, or writing HTML.

### Action Items
1. **Define Canvas Aspect Ratio**:
   * Vertical Reel / TikTok / Shorts: `1080×1920` (9:16).
   * Cinematic Landscape / YouTube: `1920×1080` (16:9).
2. **Partition the Video into Atomic Pages**:
   * Calculate exact start/end timecodes for every screen.
   * Apply the **Pacing Formula**:
     $$\text{Word Budget} = (\text{Page Duration in Seconds} - \text{Negative Space Margin}) \times 2$$
   * For a **5.0-second page**: Budget **8 to 10 words maximum**, leaving **0.5s–0.8s tail silence** for visual processing and transition sound effects.

### The Page-by-Page Production Matrix
| Page # | Screen Role | Timecode Window | Duration | Psychological Shift / Visual Event | Max Word Budget | Tail Margin |
| :---: | :--- | :---: | :---: | :--- | :---: | :---: |
| **P01** | The Provocative Hook | `0.0s – 5.0s` | 5.0s | Real parents video ➔ red `REJECTED` stamp slam | 9 words | 0.8s |
| **P02** | The Dilemma / Contrast | `5.0s – 11.0s` | 6.0s | Top: Static 2D brochure vs Bottom: Live 360° twin | 11 words | 0.6s |
| **P03** | System Architecture | `11.0s – 17.0s` | 6.0s | 3-node glass pipeline revealing the tech engine | 10 words | 0.7s |
| **P04** | Immersive Proof | `17.0s – 23.0s` | 6.0s | Fullscreen aerial flythrough with glass HUD pill | 10 words | 0.5s |
| **P05** | Interactive Action | `23.0s – 29.0s` | 6.0s | iPhone WhatsApp chat with animated live typing | 10 words | 0.6s |
| **P06** | Institutional Authority | `29.0s – 34.0s` | 5.0s | 8 accredited campus logos & trust badges | 8 words | 0.5s |
| **P07** | Call to Action Closer | `34.0s – 38.0s` | 4.0s | Specular brand logo reveal with pulsing CTA button | 7 words | 0.8s |

---

### Media & Motion Classification (Part of Stage 1 `PLAN.md`)

**Goal**: Determine the exact visual medium and asset pipeline for every individual page to eliminate guesswork before **Gate 1**.

### Classification Categories
Assign each page to one of four technical pipelines:
1. **Pure Motion Infographics**: 100% HTML/CSS/GSAP vectors, metric counters, clean typography or glass cards. (Zero footage needed).
2. **Curated Video Footage**: Real human footage, campus tours, aerial drones, device recordings.
3. **AI / Google Flow Generation**: Hyper-specific cinematic scenarios generated via Google Flow or text-to-video tools.
4. **Hybrid Split / Layered Composition**: Live video background with clean unboxed overlay type or HUD callipers.

### Page Asset Classification Sheet
| Page # | Classification | Primary Visual Element | Source / Production Tool | Asset File |
| :---: | :--- | :--- | :--- | :--- |
| **P01** | Hybrid Video + Overlay | Parents reaction video + animated SVG `REJECTED` stamp | Google Flow / Stock + CSS SVG | `parents_worried_cfr.mp4` |
| **P02** | Split Hybrid Card Stack | Top: Static 2D photo card. Bottom: Live 360° campus tour | Photo capture + Drone MP4 | `flat_campus.jpg` & `students_walk_cfr.mp4` |
| **P03** | Pure Motion Infographic | Glass node graph with connecting pulsing data beams | GSAP SVG / Lucide Icons | 100% Code (Zero external video) |
| **P04** | Curated Video + HUD UI | Fullscreen drone footage with telemetry pill overlay | 4K Drone clip + CSS glass badge | `aerial_campus_cfr.mp4` |
| **P05** | Kinetic UI + Foley | Glass iPhone WhatsApp chat with typing bubble dots | Custom CSS Chat + iOS haptic taps | 100% Code + `sfx_mobile_typing_ios.wav` |
| **P06** | Pure Motion Infographic | Authority ticker with partner logo glass badges | Tailwind CSS Grid + Lucide | 100% Code (SVG Badges) |
| **P07** | Brand Motion Closer | Clean brand emblem with horizon perspective grid | Clean SVG + subtle perspective floor | Brand SVG Logo |

> [!IMPORTANT]
> ### 🛑 GATE 1: Master 5-Track `PLAN.md` Approval
> **Present the complete `PLAN.md` (Page Matrix, Media Classification, Reference Takeaway, Original Visual System, and Master Audio Plan for VO/SFX/BGM) to the user.**  
> *Do not write preview code, generate Flow clips, synthesize audio, or render video until Gate 1 is approved.*

---

## Stage 2. Playable rough cut and approval

Use the [shared editing workflow](skills/video-editing/SKILL.md) for the preview. Show the layout, sequence, motion and actual transitions in one playable timeline or low-resolution draft. Include dialogue or scratch VO, SFX and relevant ambience with background music muted. Reuse the current project. Substitute a timed label when media is missing.

**Gate 2**. Present the cut and wait for approval. Revisit changed intervals with surrounding context. The following implementation example applies when the approved composition uses HTML and GSAP.

### Modular Viewport Architecture
Every page is wrapped in its own isolated viewport container with absolute coordinates:
```html
<!-- Page 01 Viewport -->
<div id="page-01-viewport" class="page-container" style="position: absolute; inset: 0; opacity: 1;">
  <div class="video-card-frame">
    <video id="clip-p01" class="clip" data-start="0.0" data-duration="5.0" data-track-index="0"
           src="assets/clips/parents_worried_cfr.mp4" muted playsinline></video>
  </div>
  <div id="overlay-p01" class="stamp-overlay">...</div>
</div>

<!-- Page 02 Viewport -->
<div id="page-02-viewport" class="page-container" style="position: absolute; inset: 0; opacity: 0;">
  <div class="col-card-flat">...</div>
  <div class="col-card-twin">
    <video id="clip-p02" class="clip" data-start="5.0" data-duration="6.0" data-track-index="0"
           src="assets/clips/students_walk_cfr.mp4" muted playsinline></video>
  </div>
</div>
```

### Motion Isolation Rules
1. **Never Animate `<video>` Directly**: Apply GSAP scaling, rotation, blur, and opacity changes to the parent `#page-XX-viewport` or wrapper card, never to the `<video>` element.
2. **Master GSAP Timeline**: Register a single paused master timeline where pages transition cleanly:
   ```javascript
   const tl = gsap.timeline({ paused: true });
   // Page 1 -> Page 2 transition at 5.0s
   tl.to("#page-01-viewport", { opacity: 0, duration: 0.4 }, 4.8);
   tl.to("#page-02-viewport", { opacity: 1, duration: 0.4 }, 5.0);
   window.__timelines = { main: tl };
   ```

---

## Stage 3: Footage Sourcing, Clip Mapping & Closed-GOP CFR Prep *(🛑 Gate 3)*

**Goal**: Organize, approve, and pre-transcode footage cleanly before audio sync or video render.

### Action Items
1. **Confirm Real vs. Staged vs. Google Flow Clips** (no paid Flow generation without user sign-off).
2. **Pre-Transcode Every Clip to Closed-GOP CFR (`fps=30`, `-an`)**:
   ```bash
   ffmpeg -y -i "raw_footage/clip_p01.mp4" \
     -map 0:v:0 -vf "fps=30" -c:v libx264 -preset fast -crf 18 -pix_fmt yuv420p \
     -g 30 -keyint_min 30 -sc_threshold 0 -flags +cgop -fps_mode cfr -movflags +faststart \
     -an "assets/clips/clip_p01_cfr.mp4"
   ```
3. **Map Clips to `<video>` Viewport Containers (`data-media-start`, `muted playsinline`, pre-primed)**.

> [!IMPORTANT]
> ### 🛑 GATE 3: Footage Plan Approval
> **Confirm page-by-page clip mapping (`Flow` / B-roll / reused CFRs) with the user before proceeding to Stage 4 Audio Production.**

---

## Stage 4: Voice Agent — Isolated Voiceover & Timing Lock *(🛑 Gate 4)*

**Goal**: Synthesize voiceover per page, analyze quality & timings independently, obtain approval, and **lock final page cut timestamps so Stage 5 SFX aligns to reality — never script guesses**.

### Voice Direction Standards
* **Default Voice**: `en-US-AvaNeural` (Warm, authoritative, articulate female documentary voice).
* **Speed Rate**: `+8%` ceiling target (Measured, natural pace; never exceed `+8%` target / `+10%` hard max—edit copy instead).
* **Page-by-Page Sentence Rules**:
  * Every page receives **one clean sentence or thought**.
  * Spoken audio must finish **0.5s–0.8s before the page ends** (`tail silence` prevents collision during transitions).
  * Use deliberate commas (`,`) for 150ms–250ms natural breathing pauses.
* **Audio Standard**: **48,000 Hz, 24-bit PCM WAV** (`-c:a pcm_s24le`).

### Illustrative Streaming Synthesis & Individual VO Analysis (`projects/<name>/tools/produce_*_narration.py`)
- Generate discrete `vo_page_01.wav..` using `edge_tts.Communicate(..., boundary="WordBoundary")`, strip leading silence cleanly, shift `words` JSON timestamps, and warn if any spoken scene yields an empty word list.
- **Individual VO Analysis**: Print actual duration per page, WPM, LUFS/TP, and `WordBoundary` coverage.
- **Timeline Lock**: Adjust HTML/GSAP transition timestamps (`T1..Tn`) to match approved VO durations + tail breathing space **before starting Stage 5**.

> [!IMPORTANT]
> ### 🛑 GATE 4: Voiceover Audition Approval (Do Not Proceed Without User Sign-Off)
> **Deliver isolated VO narration (`voiceover_clean_narration.wav/.mp3` + per-page timing table).**  
> *Only after the user approves the voiceover and locked scene timings does Stage 5 (SFX) begin.*

---

## Stage 5: Sound Designer — Isolated SFX & Foley Locked to Animation *(🛑 Gate 5)*

**Goal**: Build tactile, cinematic sound design synchronized against the **actual VO-locked UI animation preview or rough cut** (never estimated from script), organized in 3 separate folders and audited cleanly on its own.

### Cross-Device Translation (The 3-Layer Impact Principle)
For key visual events (stamps, reveals, drops), ensure impacts contain:
1. **Sub Weight ($60–100\text{ Hz}$)**: Chest weight for headphones/TV.
2. **Harmonic Mid Body ($400\text{ Hz}–1.2\text{ kHz}$)**: Low-mid punch triggering the "phantom fundamental" on laptops/TV.
3. **Mechanical Transient Snap ($2.5–5\text{ kHz}$)**: Crisp `30ms–50ms` tactile transient cutting cleanly on mobile speakers.
*Enforce `-10 to -15 dBFS` RMS per stem, `np.argmax` peak-anchored slicing, `1.5s–3.0s` negative space, and separate `01_page_transitions/`, `02_motion_elements_and_graphics/`, `03_animations/` WAV outputs.*

### Example Sound Design Cue Matrix (`-10 to -15 dBFS RMS` Stems)
| Page # | Visual Event Trigger | SFX Category | Audio File | Trim / Edit Rule | Stem RMS Target |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **P01** | `0.00s`: Opening Hook Sweep | `01_page_transitions` | `whoosh_sub_in.wav` | Peak-anchored `argmax` | `-12 dBFS` |
| **P01** | `1.25s`: Rejection / Split Snap | `03_animations` | `stamp_slam_impact.wav` | Keep transient body + `-2 dB` pocket if VO | `-11 dBFS` |
| **P02** | `4.44s`: Toggle / Wipe Sweep | `01_page_transitions` | `card_slide_snap.wav` | Trim tail + `10ms` cosine fade | `-12 dBFS` |
| **P03** | `11.16s`: Telemetry Tick / Chime | `03_animations` | `node_connect_tech.wav` | Crisp `40–120ms` tick, `-10 to -15 dBFS` | `-13 dBFS` |

> [!IMPORTANT]
> ### 🛑 GATE 5: Isolated SFX & Foley Approval (Do Not Proceed Without User Sign-Off)
> **Deliver combined `sfx_only.wav/.mp3` + 3-bucket breakdown + Individual SFX Analysis (`argmax` peak sync error, `-10 to -15 dBFS` RMS check, dialogue clash check).**  
> *Wait for user approval before Stage 6 Background Music.*

---

## Stage 6: Music Agent — Background Music (`BGM`) Selection & Carving *(🛑 Gate 6)*

**Goal**: Select or generate instrumental music aligned to domain emotion and BPM/drop phrasing, shaped so voiceover always sits in clear focus.
- Match genre/BPM to brief (`95–115 BPM` architectural tech-house for B2B spatial, warm piano/sub for healthcare, organic swell for hospitality — **strictly instrumental, zero vocals**).
- Apply speech-presence EQ carve (`highpass=85Hz, lowpass=8500Hz`) and prepare cut-aligned breakdown/drop markers.
- **Individual BGM Analysis**: Verify LUFS/crest factor, `300Hz–3kHz` vocal headroom, and smooth outro decay.

> [!IMPORTANT]
> ### 🛑 GATE 6: Background Music Approval
> **Deliver `bgm_carved_preview.wav/.mp3` with structural timing notes (`Intro` / `Breakdown` / `Drop` / `Outro`) and wait for approval before Stage 7 mixing.**

---

## Stage 7: Audio Mixing Engineer — 5-Stem Mixdown (`48 kHz · 24-bit WAV`)

**Goal**: Combine all **5 isolated, user-approved stems** cleanly into a cohesive broadcast mix:
* **Stem 1: Voiceover (`VO`)** — Center-panned, clean speech presence.
* **Stem 2: Background Music (`BGM`)** — Stereo width with `220ms` cosine sidechain ducking (`-20.4 dBFS` / `0.095` under VO → `-8.4 dBFS` / `0.380` in breaks/outro).
* **Stem 3: Sound Effects (`SFX`)** — Peak-locked transition sweeps & hits (`-10 to -15 dBFS` RMS).
* **Stem 4: Foley** — Subtle tactile micro-sounds (`-2.5 dB / 70ms` pocket if overlapping speech).
* **Stem 5: Ambience** — Subtle spatial bed (`-28 dBFS`) when appropriate.
* **Two-Pass EBU R128 Normalization (`-c:a pcm_s24le`)**: **`-14.0 LUFS (±0.5)`**, **`TP <= -1.0 dBTP`**, **`LRA <= 7.0 LU`**, saved as **`master_audio_ebur128.wav` (`48 kHz · 24-bit PCM WAV`)**.

---

## Stage 8: Cross-Device Audio Testing & Independent Quality Review *(🛑 Gate 7)*

**Goal**: Prove the combined audio master translates flawlessly across every playback device and passes an independent critical audit **before touching video integration**.

### 1. 5-Profile Cross-Device Diagnostic Matrix
```bash
# 1. Mobile Phone Mono (250Hz - 7kHz, -ac 1 outside -af)
ffmpeg -y -i "audio/master_audio_ebur128.wav" -af "highpass=f=250,lowpass=f=7000" -ac 1 "audio/qa_mobile_mono.mp3"
# 2. Laptop Speakers (160Hz - 12kHz)
ffmpeg -y -i "audio/master_audio_ebur128.wav" -af "highpass=f=160,lowpass=f=12000" "audio/qa_laptop.mp3"
# 3. Television / Living Room (60Hz - 14kHz + verify LRA <= 7.0 LU)
ffmpeg -y -i "audio/master_audio_ebur128.wav" -af "highpass=f=60,lowpass=f=14000" "audio/qa_tv.mp3"
# 4. Headphones Full-Band (`master_audio_ebur128.wav` inspected directly across 20Hz-20kHz)
# 5. True Mono Fold-Down (Full-band -ac 1 LUFS/phase drop check)
ffmpeg -y -i "audio/master_audio_ebur128.wav" -ac 1 -af "ebur128=peak=true" -f null -
```

### 2. Independent Quality Review Audit
- Zero vocal masking (every spoken syllable clear on Mobile, Laptop, TV, Headphones, and Mono).
- Zero digital clipping (`TP <= -1.0 dBTP`), zero clicks, zero distortion, zero sub rumble.
- Exact creative & temporal alignment against Stage 4–5 cut frames. Fix any flaw at the stem level and re-export WAV before proceeding.

> [!IMPORTANT]
> ### 🛑 GATE 7: Approved Audio Master (`48 kHz · 24-bit WAV`)
> **Present combined master WAV/MP3 + Cross-Device QA metrics for final user approval. Never render/mux final MP4 with unapproved audio.**

---

## Stage 9: Video Assembly Render, Fast `0.5s` Audio Integration & Final Delivery QA

**Goal**: Render the **Gate 2 + Gate 4 timing-locked** HyperFrames composition (`raw_video.mp4`), integrate the **Approved `48 kHz · 24-bit WAV` Audio Master**, and audit the finished MP4.

### 1. Final Visual Render & Key-Frame Verification
```bash
npx hyperframes check "projects/<project_name>"
npx hyperframes render "projects/<project_name>" -o "export/<project_name>/raw_video.mp4" -q looks --format mp4
```
Extract representative key-frame stills across every page (`P01..Pn`) and verify smooth playback with zero frozen frames or visual glitches.

### 2. Fast `0.5s` Audio-to-Video Integration (Stream Copy)
```bash
# Multiplex Approved Audio Master onto rendered video in ~0.5 seconds
ffmpeg -y \
  -i "export/<project_name>/raw_video.mp4" \
  -i "projects/<project_name>/audio/master_audio_ebur128.wav" \
  -map 0:v:0 -map 1:a:0 \
  -c:v copy \
  -c:a aac -b:a 320k -ar 48000 \
  -shortest \
  "export/<project_name>/master_deliverable.mp4"
```
*(Because video visuals are separate from audio mastering, audio tweaks only re-run Stage 7–8 + this 0.5s mux without re-rendering video frames.)*

---

## Delivery Quality Assurance Checklist (Page-by-Page Audit)

Before finalizing any video deliverable:

- [ ] **Page Continuity**: Verified seamless transitions from Page $N$ to Page $N+1$ without visual flickers or `1 -> 0 -> 1` opacity pops.
- [ ] **Loudness & True Peak Audit**: Ran `ffmpeg -i master_deliverable.mp4 -af ebur128=peak=true -f null -` and verified **`-14.0 LUFS (±0.5)`** and true peak $\le$ **`-1.0 dBTP`**.
- [ ] **Delivered MP4 Speech & SFX Audit**: Inspected the actual muxed **delivered MP4** (listen or transcribe + check cue offsets) to confirm opening/closing narration is crisp and every key SFX lands cleanly on its intended visual cue (numeric loudness alone does not catch dropped dialogue).
- [ ] **Mobile & Mono Simulation**: Auditioned via mobile filter (`ffmpeg -i master_deliverable.mp4 -af "highpass=f=250,lowpass=f=7000" -ac 1 -f null -` or written mono MP3) with `-ac 1` placed **outside** `-af` to confirm SFX cut through dialogue on phone speakers without phase cancellation.
- [ ] **Continuous Motion**: Confirmed no frozen frames or decoder stalls on any page.
- [ ] **Sync Verification**: Checked kinetic text highlighting against spoken words page-by-page.
- [ ] **Clarity & Separation**: Confirmed music ducks cleanly beneath dialogue with zero vocal masking.
- [ ] **Deliverable Package**: Provided master MP4, master 48kHz 24-bit WAV (`-c:a pcm_s24le`), audition MP3, and scene snapshot proofs for every page.
