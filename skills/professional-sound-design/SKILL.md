---
name: professional-sound-design
description: >-
  Professional sound design, SFX planning, transient-accurate trimming, silence removal,
  negative space management, Web Audio mixing, dynamic ducking, and broadcast EBU R128 audio mastering
  (-14 LUFS, -1 dBTP ceiling) for HyperFrames and AI video projects. Use whenever a video requires SFX, audio mixing,
  cinematic impacts, UI sounds, or loudness mastering.
---

# Professional Sound Design & Surgical Audio Mastering for HyperFrames

This skill enforces a broadcast-grade audio engineering and sound design pipeline for AI video production in HyperFrames. It guarantees that sound effects are **surgically trimmed, transient-aligned, and mixed with intentional negative space** rather than played as raw, bloated audio files.

---

## 1. The Core Problem: Why Untrimmed SFX Fails

Standard AI video automation fails because it treats SFX as complete unedited files:
- **Leading Silence Latency**: Raw files often have 50ms–1,500ms of dead air before the sound strikes, causing the acoustic impact to lag behind the visual frame.
- **Bloated Tails**: A UI pop or click requires only 40–80ms, but files drag for 500ms–2,500ms, creating muddy overlapping clutter.
- **Lack of Negative Space**: Sound effects played continuously cause ear fatigue and bury the voiceover.

---

## 2. Mandatory SFX Preprocessing Pipeline

Every sound effect MUST pass through a 4-stage DSP pre-processing filter (via Python `scipy`, `numpy`, and `soundfile`):

```
[Raw Sound File]
       │
       ▼
1. Silence Stripping (Detect onset threshold at -30 dB; trim leading dead air to 0 ms)
       │
       ▼
2. Transient Pinpointing (Locate exact peak transient index via NumPy/SciPy)
       │
       ▼
3. Surgical Trimming (Extract only the active sound body; apply 8-15 ms cosine micro-fades)
       │
       ▼
4. Frame-Accurate Sync (Align transient peak to t_contact; enforce negative space gaps)
```

### Standard Duration Caps by Sound Type

| Sound Category | Maximum Active Duration | Trimming Rule |
| :--- | :---: | :--- |
| **UI Click / Tap** | **`50 – 120 ms`** | Strip leading silence; hard cut tail at 100ms with a 10ms micro-fade. |
| **Text Pop / Badge** | **`80 – 180 ms`** | Isolate initial pop transient (35ms) + short 60ms decay; kill ringing. |
| **Airy Whoosh / Swipe** | **`200 – 380 ms`** | Align peak transient to cut frame; anticipation ramp starts −180ms early. |
| **Confirmation Chime** | **`350 – 600 ms`** | Strip leading dead air; start on bell strike; fade tail after 500ms. |
| **Negative Space** | **`≥ 250 ms gap`** | Mandatory silence buffer between non-layered effects. |

---

## 3. Frame-Accurate Transient Synchronization

Never align the *beginning of an unedited sound file* to an animation timestamp:
1. **Impact / Contact Cues (Clicks, Pops, Button Presses)**:
   - Align the **peak transient** exactly to `t_contact` (0ms error).
2. **Motion / Transition Cues (Whooshes, Swipes)**:
   - Calculate the rise time: `t_rise = t_peak - t_onset`.
   - Start playback at `t_contact - t_rise` so the acoustic crest lands exactly on frame 0 of the new scene.

---

## 4. Negative Space & Overlap Management

1. **Maximum SFX Density**: No more than **4 to 8 total SFX cues per 30 seconds** of video.
2. **Active Sound Ratio**: Active SFX time should occupy **less than 10%** of the total video duration.
3. **No Wall-of-Sound**: Leave at least **1.5 to 2.5 seconds of clean negative space** between cues so the narration breathes.

---

## 5. Broadcast EBU R128 Audio Mastering Specification

All exported social reels and broadcast videos must meet these technical metrics:

| Metric | Target Specification | Enforcement Filter |
| :--- | :--- | :--- |
| **Integrated Loudness** | **−14.0 LUFS** (±0.5 LUFS) | FFmpeg `loudnorm=I=-14:TP=-1.0:LRA=7` |
| **Maximum True Peak** | **−1.0 dBTP** | Prevents DAC inter-sample clipping on mobile speakers |
| **Loudness Range (LRA)**| **4.0 – 8.0 LU** | Keeps dialogue intelligible across quiet/loud environments |
| **Audio Format** | Stereo AAC @ 256 kbps, 44.1/48 kHz | Broadcast standard delivery |

---

## 6. Pre-Placement SFX Cue Sheet Protocol

Before mixing, every video project must produce an audited Cue Sheet:

```markdown
| ID | Timestamp | Visual Impact Point | Category | Trimmed Dur | Gain | Negative Space |
| :---: | :---: | :--- | :--- | :---: | :---: | :---: |
| `SFX-01` | `00.10s` | PDF scroll on phone | Friction | `120 ms` | `0.20` | `2.8s clean gap` |
| `SFX-02` | `03.10s` | Match-cut to 8K Lab | Sweep | `220 ms` | `0.18` | `6.2s clean gap` |
| `SFX-03` | `09.50s` | Smart Classrooms tap | UI Tap | `50 ms` | `0.16` | `2.0s clean gap` |
```

## 7. Field-Tested Engineering Guardrails (From Reel 03)

- **Always Probe Peak Index (`argmax`) Before Slicing**: Source cinematic whooshes and risers vary widely in buildup time (e.g., `2.5s–4.0s` before peak). Never hardcode `start_offset_s` blindly; extract symmetric pre/post windows anchored around the measured peak so transition crests hit frame 0.
- **Audible UI Staging (`-10 to -15 dBFS RMS` per stem)**: Short `50–120ms` micro UI hits drop out on mobile/laptop speakers if left at `-22 dBFS` RMS next to bass impacts. Level micro hits cleanly with warm mid-band harmonic presence and apply gentle dynamics + true-peak limiting before export.
- **Separate Categorized Deliverables**: Organize individual 48kHz 24-bit `.wav` cues under `01_page_transitions/`, `02_motion_elements_and_graphics/`, and `03_animations/` with a JSON audit manifest, plus a combined `sfx_only` WAV/MP3 audition stem.
- **Prevent MP3 Inter-Sample Overshoots**: Verify the rendered `.wav` and `.mp3` stems with FFmpeg `ebur128=peak=true` and `volumedetect`; enforce `TP <= -1.0 dBTP` via two-pass `loudnorm` rather than relying solely on a non-oversampled limiter.
