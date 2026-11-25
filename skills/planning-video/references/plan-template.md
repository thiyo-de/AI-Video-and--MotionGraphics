# Video Production Master Plan — `<PROJECT_TITLE>`

- **Format & Specs**: `1080×1920 (9:16)` · `30 fps` · `<30.0s>` total
- **Audience & Goal**: `<Audience>` → `<Conversion Action>`
- **Core Contrast**: `<Old Pain>` vs. `<New Proof>`
- **Visual System**: Dark Obsidian/Aurora `#070B15` · Accent `<#FF791F / #38BDF8>` · Fonts `Google Sans` + `Satoshi` (`0` italic) · **~50% Footage / ~50% Motion UI**

---

## Page-by-Page Narrative Spine (`P01..Pn`)

| Page | Role | Window | Dur | Core Beat & Emotional Shift | Transition Out |
| :--- | :--- | :---: | :---: | --- | :--- |
| `P01` | Hook (Pattern Interrupt) | `0.0s–4.0s` | `4.0s` | `<Visual interrupt + contrast title>` | `<e.g. Z-Pullback>` |
| `P02` | Problem / Reframe | `4.0s–7.0s` | `3.0s` | `<Reordered preview cards + monolith>` | `<e.g. Match-Cut Zoom>` |

---

## 1. Flow Clips / Video Clips

| Page | Asset ID | Source Pipeline | Clip Window / Continuity | Dimensions & Speed | Google Flow Prompt / Capture Direction |
| :---: | :--- | :--- | :--- | :--- | --- |
| `P01` | `clip_01.mp4` | `Google Flow` / `B-roll` | `0.00s -> 4.15s` (Master) | `1080×1920`, `1.5×` | `<Subject, framing, camera move, lighting, NO text>` |
| `P02` | `clip_01.mp4` (PiP) | `Reused Master` | `data-media-start="3.85"` | `1080×1920`, `1.5×` | Seamless continuation from `P01` dock |

---

## 2. Motion Graphics & UI Architecture

| Page | Motion Role | Catalog / Reference Source Used | DOM Elements & Transform Specs (No `.add()` Text Swaps) |
| :---: | :--- | :--- | --- |
| `P01` | Masked Kinetic Hook | Custom GSAP / `pv-motion` (`PV.rise`) | `<.k-mask` `yPercent: 115 -> 0`, pure GPU transforms> |
| `P02` | Bento Cards & Match-Cut | `herk` 4-stop liquid-glass / `motion-pack-3` | `<Pre-ordered static cards `#t1..t3`, `calc()` / `xPercent` steppers> |

---

## 3. Voiceover (`VO`) Plan

- **Voice & Pace**: `<en-US-AvaNeural>`, `130–145 WPM` (`<= 2.2 words/sec`, rate `<= +11%`)

| Scene | Start–End (`s`) | Tail Gap | Script Line (TTS Pronunciation Safe) | Words |
| :---: | :---: | :---: | --- | :---: |
| `s01` | `0.22s–2.60s` | `1.40s` | `"..."` | `8` |
| `s02` | `4.05s–6.10s` | `0.90s` | `"..."` | `5` |

---

## 4. Sound Effects (`SFX`) Cue Sheet

- **Master Rule**: All cues peak-anchored (`argmax` for sweeps, `0ms` onset for impacts), `-10 to -15 dBFS` RMS per stem, output separated into `01_page_transitions/`, `02_motion_elements_and_graphics/`, `03_animations/` + combined `sfx_only.wav`.

| Cue ID | Bucket | Trigger Timestamp | Peak Align / Dur | Visual Event | Vocal Pocket Needed? |
| :--- | :--- | :---: | :---: | --- | :---: |
| `PT-01` | `01_page_transitions` | `0.00s` | `450ms` sweep | Scene 01 open air sweep | No |
| `MG-01` | `02_motion_elements_and_graphics` | `4.02s` | `0ms` slam | Hero monolith + glass dock | No |
| `AN-01` | `03_animations` | `0.35s` | `115ms` punch | Kinetic word pop | No |

---

## 5. Background Audio (`BGM`) Plan

- **Track Style & Selection Reason**: `<Genre / mood / instrumentation tailored to brief; instrumental only>`
- **Tempo & Structure**: `<BPM>` · Intro `0.0s–<X>s` · Breakdown `<X>s–<Y>s` · Drop `<Y>s` · Natural Fade `<Z>s–30.0s`
- **Frequency & Ducking Curve**: `highpass=85Hz, lowpass=8500Hz` under VO; ducked to `0.085–0.12` during speech, rising to `0.20–0.40` across open hooks/outro with `220ms` cosine ramps.
- **Final Broadcast Target**: Two-pass EBU R128 `loudnorm` → **`-14.0 LUFS`**, **`-1.0 dBTP`**, **`LRA <= 7.0 LU`**.

---

## Checkpoint Approval
- [ ] Track 1 Flow/Video Prompts approved
- [ ] Track 2 Motion/Template picks approved
- [ ] Track 3 VO phrasing & cadence approved
- [ ] Track 4 SFX 3-bucket cue sheet approved
- [ ] Track 5 BGM mood & ducking profile approved
