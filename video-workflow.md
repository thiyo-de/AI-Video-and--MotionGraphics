# ⚡ Studio Video Production Workflow (SOP)

> **Standard Operating Procedure for Fast, Error-Free AI Video Creation**  
> **Complements**: [ai-video-editing.md](file:///d:/AI%20Video%20Editing/AI%20Video%20Editing/ai-video-editing.md)  
> **Core Philosophy**: **Preview-First, Render-Last.** Zero wasted render cycles.  
> **Governing Architecture**: **Strictly Page-by-Page (Screen-by-Screen).** Every single production asset, layout, voiceover line, and sound effect is authored and reviewed as an atomic page before whole-timeline assembly.  
> **Origin**: Battle-tested and refined during the production of [ruthram360_campus_closer_mastered.mp4](file:///D:/AI%20Video%20Editing/export/reels_9x16/ruthram360_campus_closer_mastered.mp4).

---

> [!IMPORTANT]
> ## 🛡️ The Fundamental Law: Everything is Page-by-Page
> A video is **never** authored or processed as an uncontrollable 30-second or 60-second monolithic block.  
> A high-end video is an assembly of discrete, atomic **Pages (Screens)**.  
>
> **Every single Page is an independent creative unit** with 6 fixed parameters:
> 1. **Timecode & Duration Window**: Exactly defined start and end seconds (e.g. Page 1: `0.0s – 5.0s`, Page 2: `5.0s – 11.0s`).
> 2. **DOM Viewport Container**: Independent wrapper (`<div id="page-01-viewport">`) preventing transform bleed.
> 3. **Unique Layout & Motion**: Dedicated card glassmorphism, metric counters, badges, and kinetic typography.
> 4. **Assigned Media Asset**: Specific CFR-transcoded video clip or static graphic mapped to that page.
> 5. **Dedicated Voiceover Sentence**: Word-budgeted narration line (strictly $\le 2\text{ words/sec}$) with breathing silence.
> 6. **Tailored SFX & Foley Cues**: Transition sweep entering the page, tactile foley during page action, and exit cues.
>
> **You never render a full video until every individual page has been validated through this 7-step sequence.**

---

## The 7-Step Page-by-Page Production Pipeline

```
[Step 1: Page-by-Page Narrative Blueprint] ──────────► 🛑 CHECKPOINT 1: Story & Time Budget Alignment
                 │
[Step 2: Page-by-Page Media Classification] ────────► 🛑 CHECKPOINT 2: Asset Strategy Alignment
                 │
[Step 3: Page-by-Page DOM & Motion Layout]
       └── [Step 3.1: Interactive Page Layout Widget (NO Video Render)] ──► 🛑 CHECKPOINT 3: Screen-by-Screen UI Approval
                 │
[Step 4: Page-by-Page Clip Mapping (NO Video Render)] ───────────────► 🛑 CHECKPOINT 4: Footage Plan Approval
       └── [Step 4.1: Closed-GOP Transcode & Video Assembly Render] ────► 🛑 CHECKPOINT 4.1: Visual Motion Verification
                 │
[Step 5: Page-by-Page Narration Synthesis (AvaNeural / Calm / Punctuation)]
                 │
[Step 6: Page-by-Page Surgical SFX & Foley Design]
       └── [Step 6.1: Page-by-Page Isolated VO & SFX Audition Stems] ──► 🛑 CHECKPOINT 6: Audio Stems Audition
                 │
[Step 7: Master Timeline Stitching, 5-Stem Mix & 0.5s Fast Remux] ──► 🚀 FINAL DELIVERABLE & QA
```

---

## Step 1: Page-by-Page Narrative Blueprint & Time Budgeting

**Goal**: Partition the total video runtime into discrete, bite-sized Pages (Screens) with defined psychological objectives and strict word budgets.

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

> [!IMPORTANT]
> ### 🛑 CHECKPOINT 1: Story & Time Budget Alignment
> **Present the Page-by-Page Production Matrix to the user.**  
> *Do not write code, build layouts, or record audio until the user approves the page sequence and durations.*

---

## Step 2: Page-by-Page Media & Motion Classification

**Goal**: Determine the exact visual medium and asset pipeline for every individual page to eliminate guesswork.

### Classification Categories
Assign each page to one of four technical pipelines:
1. **Pure Motion Infographics**: 100% HTML/CSS/GSAP vectors, metric counters, glowing glass cards, kinetic typography. (Zero footage needed).
2. **Curated Video Footage**: Real human footage, campus tours, aerial drones, device recordings.
3. **AI / Google Flow Generation**: Hyper-specific cinematic scenarios generated via Google Flow or text-to-video tools.
4. **Hybrid Split / Layered Composition**: Live video background contained in a glass card with interactive UI overlay badges.

### Page Asset Classification Sheet
| Page # | Classification | Primary Visual Element | Source / Production Tool | Asset File |
| :---: | :--- | :--- | :--- | :--- |
| **P01** | Hybrid Video + Overlay | Parents reaction video + animated SVG `REJECTED` stamp | Google Flow / Stock + CSS SVG | `parents_worried_cfr.mp4` |
| **P02** | Split Hybrid Card Stack | Top: Static 2D photo card. Bottom: Live 360° campus tour | Photo capture + Drone MP4 | `flat_campus.jpg` & `students_walk_cfr.mp4` |
| **P03** | Pure Motion Infographic | Glass node graph with connecting pulsing data beams | GSAP SVG / Lucide Icons | 100% Code (Zero external video) |
| **P04** | Curated Video + HUD UI | Fullscreen drone footage with telemetry pill overlay | 4K Drone clip + CSS glass badge | `aerial_campus_cfr.mp4` |
| **P05** | Kinetic UI + Foley | Glass iPhone WhatsApp chat with typing bubble dots | Custom CSS Chat + iOS haptic taps | 100% Code + `sfx_mobile_typing_ios.wav` |
| **P06** | Pure Motion Infographic | Authority ticker with partner logo glass badges | Tailwind CSS Grid + Lucide | 100% Code (SVG Badges) |
| **P07** | Brand Motion Closer | Specular brand logo with pulsing glowing CTA button | CSS Specular gradient + Radial glow | Brand SVG Logo |

> [!IMPORTANT]
> ### 🛑 CHECKPOINT 2: Asset Strategy Alignment
> **Present the Page Asset Classification Sheet to the user.**  
> *Confirm which pages require user-supplied footage, which require AI generation, and which are pure code.*

---

## Step 3: Page-by-Page DOM & Motion Layout Construction

**Goal**: Build each page as an independent visual viewport in HTML/CSS/Tailwind, ensuring clean modular separation.

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

### Step 3.1: Interactive Page Layout Widget (NO Video Render)

**Why this saves hours**: Video rendering takes 2–5 minutes per attempt. A tabbed HTML preview widget renders **instantly in 0.0 seconds** in any browser, allowing screen-by-screen design inspection.

### Action Items
1. Generate `layout_preview_widget.html` in the conversation artifact directory or project folder.
2. Provide interactive clickable tabs for every single page:
   * `[Page 1: Hook]` `[Page 2: Dilemma]` `[Page 3: System]` `[Page 4: Proof]` `[Page 5: Action]` `[Page 6: Authority]` `[Page 7: Closer]`
3. Clicking a tab renders that exact page's layout, glassmorphic cards, typography scale (Clash Display + Satoshi), and color contrast inside a 1080×1920 mobile viewport frame.

> [!IMPORTANT]
> ### 🛑 CHECKPOINT 3: Screen-by-Screen UI Approval
> **Deliver [layout_preview_widget.html](file:///c:/Users/ADMIN/.gemini/antigravity/brain/31d64721-5bc4-46b0-b73e-deb1959af81d/layout_preview_widget.html) to the user.**  
> *Ask the user to click through every page tab, auditing typography, contrast, and layout hierarchy before rendering any video.*

---

## Step 4: Page-by-Page Footage & Clip Mapping (NO Video Render)

**Goal**: Organize, verify, and map video footage to DOM containers page-by-page before executing video renders.

### Action Items
1. **Author the Page Clip Cue Sheet**:
   | Page # | Viewport Container ID | Video Tag ID | Assigned Clip | Time In | Duration | Audio Action |
   | :---: | :--- | :--- | :--- | :---: | :---: | :--- |
   | **P01** | `#page-01-viewport` | `#clip-p01` | `assets/clips/parents_worried_cfr.mp4` | 0.0s | 5.0s | Muted (`-an`) |
   | **P02** | `#page-02-viewport` | `#clip-p02` | `assets/clips/students_walk_cfr.mp4` | 5.0s | 6.0s | Muted (`-an`) |
   | **P04** | `#page-04-viewport` | `#clip-p04` | `assets/clips/aerial_campus_cfr.mp4` | 17.0s | 6.0s | Native foley preserved |
2. **Present the Clip Checklist to the User**:
   * Confirm that each video clip fits its page's narrative intent.

> [!IMPORTANT]
> ### 🛑 CHECKPOINT 4: Footage Plan Approval
> **Confirm page-by-page clip mapping with the user.**  
> *Ensure all placeholder or stock footage is approved before starting batch transcode and rendering.*

---

### Step 4.1: Closed-GOP Transcode & Video Assembly Render

Once page clips are approved, process media and render the visual video pass:

1. **Pre-Transcode Every Clip to Closed-GOP CFR**:
   ```bash
   ffmpeg -y -i "raw_footage/clip_p01.mp4" \
     -map 0:v:0 -vf "fps=30" -c:v libx264 -preset fast -crf 18 -pix_fmt yuv420p \
     -g 30 -keyint_min 30 -sc_threshold 0 -flags +cgop -fps_mode cfr -movflags +faststart \
     -an "assets/clips/clip_p01_cfr.mp4"
   ```
2. **Render Raw Visual Composition**:
   ```bash
   npx hyperframes render "projects/<project_name>" -o "export/<project_name>/raw_video.mp4" -q looks --format mp4
   ```
3. **Extract Page-by-Page Snapshot Proofs**:
   ```bash
   # Extract keyframes from the center of each page's timecode window
   ffmpeg -y -ss 00:00:02.00 -i raw_video.mp4 -frames:v 1 -q:v 2 "export/proof_page_01.png"
   ffmpeg -y -ss 00:00:07.50 -i raw_video.mp4 -frames:v 1 -q:v 2 "export/proof_page_02.png"
   ffmpeg -y -ss 00:00:14.00 -i raw_video.mp4 -frames:v 1 -q:v 2 "export/proof_page_03.png"
   ffmpeg -y -ss 00:00:20.00 -i raw_video.mp4 -frames:v 1 -q:v 2 "export/proof_page_04.png"
   ffmpeg -y -ss 00:00:26.00 -i raw_video.mp4 -frames:v 1 -q:v 2 "export/proof_page_05.png"
   ffmpeg -y -ss 00:00:31.50 -i raw_video.mp4 -frames:v 1 -q:v 2 "export/proof_page_06.png"
   ffmpeg -y -ss 00:00:36.00 -i raw_video.mp4 -frames:v 1 -q:v 2 "export/proof_page_07.png"
   ```

> [!IMPORTANT]
> ### 🛑 CHECKPOINT 4.1: Visual Motion Verification
> **Share page-by-page snapshot proofs with the user.**  
> *Confirm that video playback is smooth, animations are timed properly, and there are no frozen video frames.*

---

## Step 5: Page-by-Page Narration Synthesis (AvaNeural / Calm & Punctuation)

**Goal**: Synthesize voiceover page-by-page with exact duration matching, natural breathing pauses, and streaming word metadata.

### Voice Direction Standards
* **Default Voice**: `en-US-AvaNeural` (Warm, authoritative, articulate female documentary voice).
* **Speed Rate**: `+11%` (Measured, natural pace; never hurried).
* **Page-by-Page Sentence Rules**:
  * Every page receives **one clean sentence or thought**.
  * Spoken audio must finish **0.5s–0.8s before the page ends** to prevent vocal collision during page transitions.
  * Use deliberate commas (`,`) to introduce natural 150ms–250ms breathing pauses.
* **Audio Standard**: **48,000 Hz, 24-bit PCM WAV**.

### Page-by-Page Narration Script & Time Alignment
| Page # | Timecode Window | Max Voice Duration | Script Sentence | Word Count |
| :---: | :---: | :---: | :--- | :---: |
| **P01** | `0.0s – 5.0s` | 4.2s | *"Every year, ninety percent of student applications get rejected."* | 9 words |
| **P02** | `5.0s – 11.0s` | 5.3s | *"Flat photos hide reality. Live digital twins reveal the truth."* | 10 words |
| **P03** | `11.0s – 17.0s` | 5.2s | *"Our platform verifies facilities, faculty, and real-world placement records instantly."* | 10 words |
| **P04** | `17.0s – 23.0s` | 5.4s | *"Tour campuses in ultra-high-definition from anywhere in the world."* | 9 words |
| **P05** | `23.0s – 29.0s` | 5.3s | *"Connect directly with verified admission counselors over WhatsApp."* | 8 words |
| **P06** | `29.0s – 34.0s` | 4.5s | *"Trusted by fifty premier universities across the nation."* | 8 words |
| **P07** | `34.0s – 38.0s` | 3.2s | *"Secure your future today with Ruthram Three-Sixty."* | 7 words |

### Streaming Synthesis Script (`tools/produce_narration.py`)
Generates discrete WAV files for each page (`audio/stems/vo/vo_page_01.wav`, `vo_page_02.wav`...) and captures exact `WordBoundary` timestamps for subtitle synchronization.

---

## Step 6: Page-by-Page Surgical SFX & Foley Design

**Goal**: Build tactile, cinematic sound design mapped page-by-page to visual cuts, kinetic element animations, and UI foley that translates cleanly across mobile speakers, laptops, and headphones.

### Cross-Device Translation (The 3-Layer Impact Principle)
For key visual events (stamps, reveals, drops), do not rely on sub-bass alone (which mobile micro-speakers cut below 200–250 Hz). Ensure key impacts contain:
1. **Sub Weight ($60–100\text{ Hz}$)**: Physical chest resonance for headphones and subwoofers.
2. **Harmonic Mid Body ($400\text{ Hz}–1.2\text{ kHz}$)**: Low-mid punch triggering the brain's "phantom fundamental" on laptops and TVs.
3. **Mechanical Transient Snap ($2.5–5\text{ kHz}$)**: Sharp $30\text{ms}–50\text{ms}$ click that cuts cleanly through spoken dialogue on phone speakers.
*Rule: Do not blanket-trim or over-process every sound. Preserve natural decay when original assets already translate well.*

### Page-by-Page Sound Design Matrix
| Page # | Visual Event Trigger | SFX Category | Audio File | Trim / Edit Rule | Mix Gain |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **P01** | `0.0s`: Reel Intro Whoosh | Transition Sweep | `whoosh_sub_in.wav` | Align peak transient to `0.0s` | `-14 dBFS` |
| **P01** | `1.2s`: Red `REJECTED` Stamp Slam | Heavy Impact | `stamp_slam_impact.wav` | **Keep full 2.2s sub decay** | `-11 dBFS` |
| **P02** | `5.0s`: Split Card Slide-In | Mechanical Swoosh | `card_slide_snap.wav` | Trim tail to 0.4s | `-18 dBFS` |
| **P03** | `11.2s`: Node Pulse Light-Up | Tech Beep / Chime | `node_connect_tech.wav` | Trim tail to 80ms | `-22 dBFS` |
| **P04** | `17.0s`: Drone Whoosh Transition | Cinematic Riser | `cinematic_swell.wav` | 0.8s swell into drone reveal | `-16 dBFS` |
| **P05** | `23.3s–25.15s`: WhatsApp Message Typing | Tactile Foley | `sfx_mobile_typing_ios.wav` | **Discrete 30ms glass haptic taps** | `-12 dBFS` |
| **P05** | `25.3s`: WhatsApp Message Send "Whoosh" | UI Foley | `message_sent_pop.wav` | Clean 50ms chime | `-15 dBFS` |
| **P06** | `29.0s`: Partner Badges Unfurl | Kinetic Rattle | `cards_deck_fan.wav` | 0.5s textured flutter | `-20 dBFS` |
| **P07** | `34.0s`: Logo Specular Flare | Shimmer Chime | `metallic_sheen_chime.wav` | Full 1.8s shimmer decay | `-16 dBFS` |
| **P07** | `36.0s`: Final CTA Button Pulse | Sub Thump | `sub_bass_drop.wav` | Full 2.0s low-end decay | `-13 dBFS` |

---

### Step 6.1: Page-by-Page Isolated VO & SFX Audition Stems

**Why separate auditioning prevents errors**: If dialogue and SFX are mixed together too early, it is impossible to hear whether an SFX is masking a spoken syllable or if speech volume is balanced against music.

### Action Items
1. Export isolated review audio files:
   * `audio/stems/voiceover_clean_narration.mp3` (Dialogue only, auditioning Pages 1–7).
   * `audio/stems/sfx_and_foley_only.mp3` (All sound design & foley without dialogue or music).
   * `audio/stems/music_bed_ducked.mp3` (Background track with ducking dips).
2. **Run Diagnostic Mobile Speaker Simulation**:
   ```bash
   # Filter master audio through a phone speaker profile (250Hz - 7kHz Mono)
   ffmpeg -y -i "audio/master_audio_ebur128.wav" -af "highpass=f=250,lowpass=f=7000" -ac 1 "audio/preview_mobile_simulation.mp3"
   ```
   *Verify that key SFX impacts remain audible and maintain positive contrast over dialogue.*
3. Present individual audition links to the user.

> [!IMPORTANT]
> ### 🛑 CHECKPOINT 6: Audio Stems Audition
> **Provide isolated audio stems to the user for listening.**  
> *Allow the user to verify speech clarity, pronunciation, and SFX impact choices page-by-page before final bus mixdown.*

---

## Step 7: Master Timeline Stitching, 5-Stem Mix & 0.5s Fast Remux

**Goal**: Combine the verified pages into the master GSAP timeline, balance the 5-stem audio bus, master to international loudness targets, and multiplex in seconds.

### 1. The 5-Stem Mixing Bus
* **Stem 1: Voiceover (VO)** — Center-panned dialogue (`0.90` gain).
* **Stem 2: Background Music (BGM)** — Stereo width with dynamic speech ducking:
  * Attenuated to **`-20.4 dBFS`** (`0.095` amplitude) under dialogue.
  * Swelled to **`-8.4 dBFS`** (`0.380` amplitude, a **`+12.0 dB`** relative boost) during musical climaxes and outro.
* **Stem 3: Sound Effects (SFX)** — Transients and cinematic impacts.
* **Stem 4: Foley** — Subtle tactile micro-sounds (typing, card flips).
* **Stem 5: Ambience** — Low-level spatial bed (`-28 dBFS`).

### 2. Mastering Target
* **Audio Standard**: ITU-R BS.1770 / EBU R128 Social Media Target.
* **Integrated Loudness**: **`-14.0 LUFS`** ($\pm 0.5$ LUFS).
* **Maximum True Peak**: $\le$ **`-1.0 dBTP`**.
* **Master WAV**: 48,000 Hz, 24-bit PCM WAV (`master_audio_ebur128.wav`).

### 3. Fast 0.5-Second Remuxing (The Iteration Superpower)
When video visuals are already rendered (Step 4.1), you **never need to re-render the video** to change narration, adjust ducking, or swap an SFX:

```bash
# Multiplex new master audio into existing raw video in 0.5 seconds
ffmpeg -y \
  -i "export/<project_name>/raw_video.mp4" \
  -i "projects/<project_name>/audio/master_audio_ebur128.wav" \
  -map 0:v:0 -map 1:a:0 \
  -c:v copy \
  -c:a aac -b:a 320k \
  -shortest \
  "export/<project_name>/master_deliverable.mp4"
```

---

## Delivery Quality Assurance Checklist (Page-by-Page Audit)

Before finalizing any video deliverable:

- [ ] **Page Continuity**: Verified seamless transitions from Page $N$ to Page $N+1$ without visual flickers.
- [ ] **Loudness Audit**: Ran `ffmpeg -i master_deliverable.mp4 -af ebur128=framelog=verbose -f null -` and verified **`-14.0 LUFS`** and $\le$ **`-1.0 dBTP`**.
- [ ] **Mobile & Mono Simulation**: Auditioned via mobile filter (`highpass=250,lowpass=7000,ac=1`) to confirm SFX cut through dialogue on phone speakers without phase cancellation.
- [ ] **Continuous Motion**: Confirmed no frozen frames or decoder stalls on any page.
- [ ] **Sync Verification**: Checked kinetic text highlighting against spoken words page-by-page.
- [ ] **Clarity & Separation**: Confirmed music ducks cleanly beneath dialogue with zero vocal masking.
- [ ] **Deliverable Package**: Provided master MP4, master 48kHz WAV, audition MP3, and scene snapshot proofs for every page.
