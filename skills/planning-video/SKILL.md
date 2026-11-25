---
name: planning-video
description: Comprehensive 5-track pre-production video planner. Analyzes the creative brief or script against the video-editing skill, workspace SOP (AI Video Editing/video-workflow.md), Google Flow MCP specs, HyperFrames 448-item registry, and cloned reference repos (herk-edit-kit, motion-pack-3, product-video-skills), then outputs a clean separated production plan across 5 tracks: (1) Flow/Video Clips, (2) Motion Graphics, (3) Voiceover (VO), (4) SFX, and (5) Background Audio (BGM) — before any credits, TTS, or renders run.
---

# Planning Video (`/planning-video`)

Architect every commercial reel, promo, or explainer **page-by-page before writing composition code, generating Flow clips, synthesizing audio, or rendering video**. This skill unifies your workspace production SOP, built-in HyperFrames registry, and curated reference repos into a deterministic, 5-track `PLAN.md` ready for sign-off.

---

## 1. Sources Consulted Before Planning

Before designing scenes or writing custom components, check existing capabilities in strict priority order:

1. **Workspace SOP, Anti-Patterns & Brand Guardrails**:
   - `d:\AI Video Editing\AI Video Editing\video-workflow.md` — Page-by-page atomic timeline, `<= 2 words/sec` VO pacing, Preview-First Render-Last checkpoints.
   - `d:\AI Video Editing\AI Video Editing\flowmcp.md` — Google Flow MCP generation guidelines, aspect ratio framing, credit-confirm safety.
   - `d:\AI Video Editing\.agents\skills\video-editing\SKILL.md` + `references/creative-direction.md`, `references/editorial-rhythm.md`, `references/production-lessons-reel03.md`.
   - `d:\AI Video Editing\.agents\skills\dont-do-in-video-edit\SKILL.md` — Mandatory anti-pattern checklist (no PowerPoint fades, no `.add()` text glitches, no `-22 dBFS` SFX drops, no fixed-px pill misalignment).
2. **Built-In HyperFrames Engine & Catalog (448 Ready Items)**:
   - `d:\AI Video Editing\.agents\skills\hyperframes\SKILL.md` — Core HyperFrames HTML/GSAP timing and render contract.
   - Always check `npx --no-install hyperframes catalog --query "<effect>"` (`hyperframes-registry`) first instead of re-coding standard transitions, cursors, charts, glass cards, or overlays.
3. **Local Cloned Reference Repos (`d:\AI Video Editing\AI Video Editing\repos\`)**:
   - **`product-video-skills/`**: Native HTML/GSAP engine (`lib/pv.js`, `lib/pv.css`), velocity-matched cuts (`PV.zoomOut/In`, `PV.whipOut/In`), 3D `PV.plane` + `PV.crop`, `.hair` calipers, auto-sizing `PV.cycle` pills, `pv-story` & `pv-music` beat-grid tools.
   - **`herk-edit-kit/`**: `MOTION_PHILOSOPHY.md` (11 Laws, perspective grid floors, 4-stop liquid-glass catchlights, light-streak cut whips, chrome text sweeps), `style-library/` (`01-vox-explainer`, `02-kallaway` cards), `style-templates/`, `video-storytelling/SKILL.md` (persistent world & camera altitudes).
   - **`motion-pack-3/`**: 10 standalone `1080x1920 @ 30fps` vertical widgets (`templates/`: `03-apple-maps-route`, `04-wastebasket-trash`, `08-toggle-flip`, `09-stat-counter`, `10-progress-bar`, `02-imessage-notification`, `01-audio-waveform`).
4. **Audio & Broadcast Mastering**:
   - `d:\AI Video Editing\.agents\skills\professional-sound-design\SKILL.md` + `AI Video Editing/repos/product-video-skills/skills/pv-music/SKILL.md` + `media-use/SKILL.md`.

---

## 2. Planning Sequence

### Step A — Concept & Atomic Page Matrix (`P01..Pn`)
1. Identify audience, conversion action, core **Pain vs. Proof** emotional contrast, aspect ratio (`1080x1920` @ `30fps` for Reels/Shorts, `1920x1080` for widescreen), and total runtime.
2. Enforce the **3-Second Hook Rule** (pattern interrupt, curiosity gap, direct callout, or visual contrast—never a slow logo intro).
3. Partition runtime into discrete atomic pages (`P01..Pn`) balancing **~50% real/Flow video footage + ~50% motion graphics/UI**.
4. Apply **Production Lessons Guardrails**:
   - Keep visual preview card sequences in exact downstream scene order (`1 -> 2 -> 3`).
   - Run the **Logo Test** (`pv-story`): every scene needs product/sector specificity, never generic placeholder slogans.

### Step B — Separate Plan Into All 5 Tracks
Output `PLAN.md` (following `references/plan-template.md`) with **5 strictly separated sections**:

#### Track 1 · Flow Clips / Video Clips (`1. flow clips / video clips`)
- Map every page `P01..Pn` to its media source: `Google Flow Video`, `Real B-roll`, `Product Capture`, or `Pure Motion (No Clip)`.
- Specify aspect ratio, clip duration needed, playback speed ramp (`1x`–`4x`), and exact **continuity offsets** (`data-media-start`) whenever a clip flows across two scenes (e.g., full-bleed hook docking into a mini PiP card).
- Write exact **Google Flow / Veo prompts** (subject, camera motion, lighting, lens, environment, **zero baked-in text/UI overlays**).

#### Track 2 · Motion (`2. motion`)
- Select reusable components/primitives before custom coding (`hyperframes catalog` IDs + exact paths inside `AI Video Editing/repos/`).
- Lock the visual design system: typography (`Google Sans` + `Satoshi`, **zero `italic`**), palette (`<= 5` functional hues, dark aurora/obsidian ground + frosted multi-stop bento cards + framed media containers).
- Specify page transitions with velocity-matched entry/exit pairs (`zoom-through`, `lateral whip`, `vertical drop`, `3D Y-axis flip`) + light streaks/blooms.
- Enforce **GSAP Determinism & Alignment Rules**:
  - Transform-only tweens (`x`, `y`, `xPercent`, `scale`, `rotateX/Y`, `opacity`, `backgroundColor` — never `letterSpacing` or `left`).
  - Pre-rendered stacked static DOM slots for multi-state HUDs (never mutate DOM text with `.add()` callbacks during transitions).
  - Proportional slider geometry (`width: calc((100% - <pad*2>) / <n>)` + `xPercent: 0 -> 100 -> 200`), never hardcoded pixels across differing stage widths.

#### Track 3 · VO (`3. vo`)
- Script line-by-line mapped to `P01..Pn` windows.
- Strictly enforce **130–145 WPM (`<= 2.2 words/sec`, `Word Budget = (Page Duration - Margin) x 2`)** and max `+8%`–`+11%` rate.
- Spell out numerals/acronyms for natural TTS pronunciation (e.g., `"Three-Sixty"`, `"eight-K H-D-R"`).
- Specify `start_sec`, `end_sec`, and mandatory `0.5s–1.4s` tail breathing silence per scene for SFX and cognitive processing.

#### Track 4 · SFX (`4. sfx`)
- Design a frame-locked Cue Sheet **pre-split into 3 functional asset buckets**:
  1. `01_page_transitions/` — air sweeps, Z-pullbacks, whip-pans, 3D orbital/axis flips, vertical drops
  2. `02_motion_elements_and_graphics/` — glass bento docks, HUD reveals, radar pin pops, framed containers, brand halos
  3. `03_animations/` — masked word punches, staggered card pops, specular glass sheens, gyro drags, shutter flashes, stepper chimes
- Require **peak-anchored slicing** (`argmax` centered for sweeps, `0ms` onset for impacts), mobile-audible per-stem leveling (**`-10 to -15 dBFS` RMS**, `-1.0 dBFS` peak), intentional negative space, and `-2.5 dB / 70ms` vocal pockets for mid-dialogue foley transients.

#### Track 5 · Background Audio (`5. background audio`)
- Recommend a **content-suited musical direction** based on industry & pacing:
  - *B2B Tech / 3D Flex*: Clean electronic / minimalist tech-house pulse (`95–115 BPM`), defined breakdown + Drop 2, **instrumental only (no vocals)**.
  - *Healthcare / Trust / Medical*: Warm atmospheric piano + gentle sub-bass pulse without jarring drops.
  - *Luxury Hospitality / Resorts*: Warm organic ambient-acoustic swell.
- Plan BPM / beat-grid sync (`beat-grid.mjs` / `music.json` if beat-cut), speech-presence EQ carving (`highpass=85Hz, lowpass=8500Hz`), cosine sidechain ducking (`0.085–0.12` under VO → `0.20–0.40` in open hooks/outros with `220ms` ramps), closing fade-out, and final **EBU R128 master contract (`-14.0 LUFS ± 0.5`, `TP <= -1.0 dBTP`, `LRA <= 7.0 LU`)**.

---

## 3. Approval Checkpoint (Mandatory)

1. Audit the drafted plan against `dont-do-in-video-edit/SKILL.md` before presenting.
2. Present the concise 5-Track overview + save `projects/<project-name>/PLAN.md` *(when in a project creation session)* **or** present the plan in chat when asked for analysis only.
3. **Stop cleanly for user approval** before generating Google Flow clips (`flow_generate_video`), rendering TTS voiceover, synthesizing SFX files, writing `index.html`, or running renders.
