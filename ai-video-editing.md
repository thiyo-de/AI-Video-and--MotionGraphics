# 🎬 Universal AI Video Production Standard (V2.0)
> **A Reusable Production Framework for High-End AI Video Editing, Deterministic Motion Graphics & Broadcast Audio Mastering**  
> **Complements & Implements**: [video-workflow.md](file:///d:/AI%20Video%20Editing/AI%20Video%20Editing/video-workflow.md) (The 7-Step Collaborative SOP)  
> **Applies To**: Any aspect ratio (9:16 Vertical Reels, 16:9 Cinematic Landscape, 1:1 Square, 4:5 Social) & any format (Explainers, Commercial Promos, Product Launches, UI Demos).

---

## 1. Technical Standards & Audio Specifications

```
Audio Measurement:       EBU R128 / ITU-R BS.1770
Social Media Target:     -14.0 LUFS Integrated (±0.5 LUFS)
Broadcast TV Target:     -23.0 LUFS Integrated (Cinema / Cable standard)
Maximum True Peak:       -1.0 dBTP (Prevents mobile DAC clipping)
Production Master Audio: 48 kHz, 24-bit PCM WAV (Industry Video Standard)
Delivery Audio:          AAC Stereo (320 kbps @ 48 kHz)
Master Video:            Constant Frame Rate (CFR), Rec.709, YUV420p
```

---

## 2. System & Environment Infrastructure

| Layer | Standard | Purpose |
| :--- | :--- | :--- |
| **Node.js Runtime** | **Node.js 22 or later** | Required by modern HyperFrames compiler and headless Chromium worker pool. |
| **Animation Engine** | `npx hyperframes` (v0.9.87+) | Frame-deterministic HTML/CSS/WebGL canvas to video compiler. |
| **Media Engine** | FFmpeg & FFprobe (v7.0+ / v9.1+) | Closed-GOP CFR encoding, audio stem mixing, two-pass loudness mastering, and remuxing. |
| **Python DSP** | Python 3.10+ / 3.12+ (in `tools/venv`) | Audio automation, multi-track buffer math, Butterworth filters, and metadata parsing. |
| **Python Libraries** | `edge-tts`, `soundfile`, `numpy`, `scipy` | Streaming neural speech synthesis, 48kHz audio manipulation, and spectral filtering. |
| **Local Speech Engine** | `whisper.cpp` (native C++ binary) | Offline speech recognition, transcription auditing, and subtitle timestamp alignment. |

---

## 3. Directory & Project Architecture

```
D:\AI Video Editing\
│
├── AI Video Editing\                        # Studio Standards & Skills Root
│   ├── ai-video-editing.md                  # This universal production blueprint (V2.0)
│   ├── video-workflow.md                    # The 7-Step Actionable Production SOP
│   └── skills\                              # Reusable Video Production Skills
│       ├── video-editing\                   # Master editing direction, rhythm & pacing
│       ├── professional-sound-design\       # EBU R128 sound design, ducking & foley
│       ├── hyperframes\                     # HyperFrames deterministic render contract
│       ├── hyperframes-registry\            # Pre-built motion blocks & components
│       └── media-use\                       # Footage, voice, audio, and asset rules
│
├── projects\<project-name>\                 # Independent Project Workspace
│   ├── index.html                           # DOM composition & GSAP master timeline
│   │
│   ├── assets\
│   │   ├── clips\                           # CFR-optimized footage (30/60 fps, Closed GOP)
│   │   ├── images\                          # Static 2D photographs, textures, UI thumbnails
│   │   └── fonts\                           # Local @font-face files (Clash Display, Satoshi, etc.)
│   │
│   ├── audio\
│   │   ├── stems\                           # 5 Independent Audio Buses
│   │   │   ├── vo\                          # Voiceover clean dialogue stems
│   │   │   ├── bgm\                         # Background music bed
│   │   │   ├── sfx\                         # Sound effects (impacts, whooshes, sweeps)
│   │   │   ├── foley\                       # Tactile interactions (typing, clicks, taps)
│   │   │   └── ambience\                    # Room tone and atmospheric beds
│   │   ├── master_audio_ebur128.wav         # Final mastered 48kHz 24-bit stereo WAV
│   │   └── sfx_cue_sheet.json               # Structured SFX decision manifest
│   │
│   └── manifests\
│       ├── edit_decisions.json              # Shot selection, duration, and pacing decisions
│       └── narration_timing.json            # WordBoundary timestamps from Edge TTS
│
├── tools\                                   # Studio Toolchain (illustrative names; real per-project scripts live under root `tools/` or `projects/<name>/tools/`)
│   ├── optimize_clips.py                    # Closed-GOP CFR FFmpeg pre-transcoder (`D:\AI Video Editing\tools\optimize_clips.py`)
│   ├── produce_*_narration.py               # Edge TTS WordBoundary streaming generator (illustrative pattern; e.g., `produce_vo_reel03.py`)
│   ├── mix_soundtrack.py                    # Multi-bus audio mixer & EBU R128 normalizer (pattern; see `master_ruthram360_audio.py`)
│   ├── render_hyperframes.py                # HyperFrames render execution wrapper
│   └── mux_and_verify.py                    # Multiplexer, AAC peak auditor & snapshot proofing (see `mux_and_verify_master.py`)
│
└── export\<project-name>\                   # Project Deliverables Destination
    ├── raw_video.mp4                        # Clean video render from HyperFrames
    └── master_deliverable.mp4               # Final video muxed with -14 LUFS master audio
```

---

## 4. HyperFrames Deterministic Render Contract

HyperFrames renders video by pausing the browser DOM and advancing it frame-by-frame: `currentTime = T - data-start`. Every project must adhere to these four core rules:

### A. Element Timing Attributes
Every timed media element must declare its time coordinates:
```html
<video id="clip-01" class="clip" data-start="5.0" data-duration="5.0" data-track-index="0" src="assets/clips/scene_02.mp4" muted playsinline></video>
```
* `data-start`: Timeline entry offset in seconds. If omitted, HyperFrames assumes `0.0s`, causing clips appearing later in the video to freeze on their last frame.
* `data-duration`: Active duration in seconds.
* `data-track-index`: Visual track lane (clips that never overlap share track `0`).

### B. The Container Wrapper Rule (Crucial for Smooth Seeking)
**Never animate transforms directly on a `<video>` element.** Animating CSS transforms on the video tag itself can cause hardware-accelerated video decoder stalls in headless Chromium.
* **Correct Structure**:
  ```html
  <!-- Animate the viewport container with GSAP; let HyperFrames manage the video -->
  <div id="facility-viewport" style="position: relative; overflow: hidden; border-radius: 28px;">
    <video id="clip-labs" class="clip" data-start="15.0" data-duration="2.0" data-track-index="0"
           src="assets/clips/labs.mp4" muted playsinline
           style="position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover;">
    </video>
  </div>
  ```

### C. GSAP Master Timeline Registration
Register the paused timeline using the composition's identifier:
```javascript
const tl = gsap.timeline({ paused: true });
window.__timelines = { main: tl };
```

### D. No Browser-Clock CSS Transitions
Never use `transition: all 0.3s` or `transition: opacity 0.5s` on seekable elements. CSS transitions run on the operating system clock, breaking frame-stepping determinism. Animate all states directly via GSAP tweens (`tl.to()`).

---

## 5. FFmpeg Video Pre-Encoding (Closed-GOP CFR Standard)

Raw AI video clips (from Google Flow, Runway, Luma) have variable frame rates and sparse 4–5 second keyframe intervals (Long GOP). They must be normalized before importing:

```bash
ffmpeg -y -i input_raw.mp4 \
  -map 0:v:0 \
  -vf "fps=30" \
  -c:v libx264 \
  -preset fast \
  -crf 18 \
  -pix_fmt yuv420p \
  -g 30 \
  -keyint_min 30 \
  -sc_threshold 0 \
  -flags +cgop \
  -fps_mode cfr \
  -movflags +faststart \
  -an \
  assets/clips/optimized_clip.mp4
```

* `-vf "fps=30" -fps_mode cfr`: Enforces strict Constant Frame Rate (eliminates dropped frame drift).
* `-g 30 -keyint_min 30 -sc_threshold 0 -flags +cgop`: Enforces **Closed GOP** with a keyframe at every 1.0 second, guaranteeing instant seeking on any frame.
* `-pix_fmt yuv420p`: Guarantees universal browser and player decode compatibility.
* **Audio Preservation**: If the clip has useful native audio, extract it to `audio/stems/foley/` before stripping with `-an`. Never discard source assets.

---

## 6. Edge TTS Voiceover Pipeline with `WordBoundary` Metadata

Rather than generating voice and redundantly transcribing it with Whisper, Edge TTS natively streams exact word boundaries during synthesis:

```python
import asyncio
import os
import json
import subprocess
import soundfile as sf
import edge_tts

VOICE = "en-US-AvaNeural" # Warm, authoritative documentary voice
RATE = "+8%"               # Natural, unhurried cadence (never exceed +8% ceiling)
SR = 48000                 # Video standard 48 kHz

async def generate_narration_with_metadata(text, scene_id, start_time, output_dir):
    os.makedirs(output_dir, exist_ok=True)
    mp3_path = os.path.join(output_dir, f"{scene_id}.mp3")
    wav_path = os.path.join(output_dir, f"{scene_id}.wav")
    json_path = os.path.join(output_dir, f"{scene_id}_timing.json")

    communicate = edge_tts.Communicate(text, VOICE, rate=RATE, boundary="WordBoundary")
    words = []

    # Stream audio data and capture word boundaries simultaneously
    with open(mp3_path, "wb") as audio_file:
        async for chunk in communicate.stream():
            if chunk["type"] == "audio":
                audio_file.write(chunk["data"])
            elif chunk["type"] == "WordBoundary":
                # Offsets in 100ns units -> convert to seconds
                offset_sec = chunk["offset"] / 10_000_000
                duration_sec = chunk["duration"] / 10_000_000
                words.append({
                    "word": chunk["text"],
                    "start": round(start_time + offset_sec, 3),
                    "end": round(start_time + offset_sec + duration_sec, 3),
                    "duration": round(duration_sec, 3)
                })

    if not words:
        print(f"[WARN] {scene_id}: WordBoundary timestamps list is empty; check edge-tts boundary flag.")

    # Save canonical word-timing manifest for animated typography
    with open(json_path, "w", encoding="utf-8") as f:
        json.dump(words, f, indent=2, ensure_ascii=False)

    # Convert to 48kHz 24-bit PCM WAV
    subprocess.run([
        "ffmpeg", "-y", "-i", mp3_path,
        "-ar", str(SR), "-ac", "2", "-c:a", "pcm_s24le",
        wav_path
    ], check=True, stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)

    data, _ = sf.read(wav_path)
    measured_duration = len(data) / SR
    print(f"✓ {scene_id}: Synthesized {len(words)} words, {measured_duration:.2f}s")
    return wav_path, words
```

### Voice Cadence & Word Budget Rules:
* **Word Budget**: Maximum **8 to 10 words per 5.0 seconds** of video. Exceeding 12 words forces uncomfortably fast pacing.
* **Negative Space Margin**: Maintain **at least 0.3s to 0.8s of silence** at the end of each slide before visual transitions.
* **Pause Control**: Commas (`,`) insert natural ~150ms pauses; periods (`.`) insert ~300ms pauses. Always measure the actual output duration.

---

## 7. Whisper.cpp: Offline Speech Recognition & Verification

Whisper is the listening counterpart to Edge TTS. In this pipeline, it is used for **audio verification** and **transcribing non-synthetic audio**:

```bash
# 1. Prepare 16kHz mono audio input
ffmpeg -y -i master_audio.wav -ar 16000 -ac 1 -c:a pcm_s16le whisper_input.wav

# 2. Extract word-level token alignment
.\tools\whisper\whisper-cli.exe -m tools\whisper\models\ggml-base.bin -f whisper_input.wav -l en -ojf -dtw base
```

* **Whisper Timestamps Note**: Whisper timestamps are **statistical estimates**, not exact millisecond ground truth. Use Edge TTS `WordBoundary` for synthetic voiceover sync, and reserve Whisper for checking pronunciation or transcribing real human recordings.

---

## 8. Multi-Stem Audio Architecture & Conditional SFX

### A. The 5 Independent Audio Buses
To prevent audio clutter and muddy frequencies, audio is grouped into 5 isolated stems:

```
[VO Stem]      ─────── Gain: 1.0 (Centered, Crisp Dialogue) ──────┐
[BGM Stem]     ─────── Dynamic Ducking (-20.4 dB under voice) ──┼──> [Master Bus] ──> EBU R128 Normalization (-14 LUFS)
[SFX Stem]     ─────── Conditional Trim / Natural Reverb Decay ───┤
[Foley Stem]   ─────── Tactile UI (30ms Haptic Screen Taps) ──────┤
[Ambience Stem]─────── Low-level Room Tone (-28 dB) ──────────────┘
```

### B. Conditional SFX Editing (Replacing Blanket Trimming)
**Never trim every SFX clip to 30–80ms.** Blanket micro-trimming destroys cinematic impacts, risers, sweeps, and natural acoustic decay.
* **UI Clicks / Keystrokes**: Trim leading silence; cut tail at 40–80ms with a 10ms micro-fade.
* **Cinematic Impacts / Drops**: Keep full natural decay (1.2s – 2.5s) to allow sub-bass frequencies to ring out cleanly.
* **Whooshes / Swipes**: Keep the 250ms–400ms anticipation ramp and align the peak transient to the visual cut frame.

### C. Cross-Device Audio Translation (The 3-Layer Impact Rule)
Loudness normalization ($-14\text{ LUFS}$) alone does **not** ensure audibility on mobile micro-speakers. For high-impact visual events (stamps, drops, reveals), ensure three complementary layers:
1. **Sub Weight ($60–100\text{ Hz}$)**: Felt on headphones and subwoofers.
2. **Harmonic Mid Body ($400\text{ Hz}–1.2\text{ kHz}$)**: Triggers the human brain's "phantom fundamental" on laptops and TVs when sub-bass is rolled off.
3. **Mechanical Transient Snap ($2.5–5\text{ kHz}$)**: Crisp $30\text{ms}–50\text{ms}$ crack that punches through dialogue on phone speakers.
*Pre-flight Test*: Filter master audio via `ffmpeg -i master.wav -af "highpass=f=250,lowpass=f=7000" -ac 1 mobile_preview.wav` to verify that SFX remain clearly audible above speech on phone hardware.

### D. Structured SFX Manifest (`sfx_cue_sheet.json`)
Every sound cue must be defined in a version-controlled JSON manifest:
```json
[
  {
    "event_id": "scene_01_stamp_slam",
    "source_file": "impact-bass-1.mp3",
    "timeline_start": 1.20,
    "decision": "KEEP_ORIGINAL_DECAY",
    "source_in": 0.0,
    "source_out": 1.80,
    "gain_dbfs": -8.4,
    "bus": "sfx",
    "reason": "Full sub-bass tail required to emphasize the rejection stamp impact"
  },
  {
    "event_id": "scene_05_whatsapp_typing",
    "source_file": "sfx_mobile_typing_ios.wav",
    "timeline_start": 23.30,
    "decision": "PROGRAMMED_HAPTIC",
    "source_in": 0.0,
    "source_out": 1.85,
    "gain_dbfs": -12.0,
    "bus": "foley",
    "reason": "Discrete 30ms mobile glass taps synchronized to typing characters"
  }
]
```

### E. Correct Decibel Gain Calculations
* Amplitude multiplier $A$ to decibels: $\text{dBFS} = 20 \cdot \log_{10}(A)$
* Decibels to amplitude: $A = 10^{(\text{dBFS} / 20)}$
* **Reference**:
  * Amplitude `0.095` = **`-20.4 dBFS`** (speech ducking bed).
  * Amplitude `0.380` = **`-8.4 dBFS`** (music swell, which is **`+12.0 dB` relative to the speech bed**).

---

## 9. Audio Mastering: EBU R128 (-23 LUFS vs -14 LUFS)

```
EBU R128 Broadcast Standard:    -23.0 LUFS (For living room TVs, soundbars, cinema)
Social Media Video Target:      -14.0 LUFS (For Instagram Reels, TikTok, YouTube, mobile speakers)
```

### Two-Pass Normalization in FFmpeg:
```bash
# Pass 1: Measure Audio Properties
ffmpeg -i rough_mix.wav -af "loudnorm=I=-14:TP=-1.0:LRA=7:print_format=json" -f null -

# Pass 2: Linear Normalization (24-bit 48 kHz PCM WAV master)
ffmpeg -y -i rough_mix.wav -af "loudnorm=I=-14.0:TP=-1.0:LRA=7.0:measured_I=<val>:measured_TP=<val>:measured_LRA=<val>:measured_thresh=<val>:offset=<val>:linear=true" -ar 48000 -ac 2 -c:a pcm_s24le master_audio_ebur128.wav
```
* **Post-Export Verification**: AAC compression can introduce true-peak overshoots. Always measure the final exported `.mp4` container using `ffmpeg -i master_deliverable.mp4 -af ebur128=peak=true -f null -` AND audition/verify delivered dialogue & SFX cues, ensuring true peak remains at or below `-1.0 dBTP`.

---

## 10. Multi-Stage Rendering & Caching Strategy

Rendering a full-resolution 1080×1920 video takes 45–75 seconds. Avoid re-rendering unnecessarily:

| Production Stage | Rendering Strategy | Command / Action |
| :--- | :--- | :--- |
| **1. Plan & Validate (`Stage 1`)** | 5-Track `PLAN.md` + Gate 1 | Lock creative brief, 5-track plan & timeline contract (`hyperframes timeline --json` after markup) |
| **2. Interactive UI (`Stage 2`)** | **Zero-Render Preview Widget + Gate 2** | Open `layout_preview_widget.html` directly in browser (`0` flicker / `0` JS errors). Zero render wait. |
| **3. Audio Pipeline (`Stages 4–8`)** | **Independent Audio Master (`Gates 4–7`)** | Build & approve separately: `VO` (locks timeline) → `SFX` (locked to animation) → `BGM` → 5-Stem Mix → **5-Device Cross-Device QA** (`48 kHz · 24-bit WAV`) |
| **4. Final Video & Remux (`Stage 9`)** | Headless Render + **0.5s Audio Mux** | Render `raw_video.mp4` (`-q looks`), mux approved `48kHz 24-bit WAV` via `-c:v copy -c:a aac -b:a 320k -ar 48000` |
| **5. Final MP4 QA (`Stage 9`)** | Delivered Container Audit | Verify `ebur128=peak=true`, `-af "highpass=f=250,lowpass=f=7000" -ac 1`, speech/SFX audition, & frame strips |

---

## 11. 21-Point Studio Quality Audit Checklist

Before delivering any video to a client or platform:

### Technical Execution
- [ ] **1. Frame Rate**: Explicit 30.0 (or 60.0) fps Constant Frame Rate (CFR).
- [ ] **2. GOP Alignment**: All source clips encoded with closed GOP (`-g 30 -flags +cgop`).
- [ ] **3. Video Tag Contract**: Every `<video>` has `class="clip"`, `data-start`, `data-duration`, `data-track-index`.
- [ ] **4. Container Animation**: Transforms animated on container wrappers, not raw `<video>` tags.
- [ ] **5. Timeline Registration**: `window.__timelines["main"] = tl;` registered with paused GSAP instance.
- [ ] **6. No CSS Transitions**: Zero browser-clock CSS transitions on animated elements.

### Audio & Sound Design
- [ ] **7. Sample Rate**: Master audio produced at **48 kHz, 24-bit PCM WAV** (`-c:a pcm_s24le`).
- [ ] **8. Integrated Loudness**: Final MP4 measures **`-14.0 LUFS (±0.5 LUFS)`** via `ebur128=peak=true`.
- [ ] **9. True Peak Ceiling**: Peak measures $\le$ **`-1.0 dBTP`** (verified on final AAC stream).
- [ ] **10. Voice Intelligibility**: Word count strictly budgeted to 8–10 words per 5-second scene, delivered MP4 listened/verified cleanly.
- [ ] **11. Edge TTS Metadata**: `WordBoundary` timestamps exported to JSON (`boundary="WordBoundary"`) with non-empty word check.
- [ ] **12. Conditional SFX**: Context-appropriate editing; cinematic tails preserved, UI clicks trimmed.
- [ ] **13. Cross-Device Translation (`Stage 8`)**: Verified approved `master_audio_ebur128.wav` & delivered MP4 across **Mobile Mono** (`-af "highpass=f=250,lowpass=f=7000" -ac 1`), **Laptop**, **Headphones**, **TV**, and **Mono Fold-down** (`-ac 1` outside `-af`).
- [ ] **14. Dynamic Ducking**: Music bed attenuates to `-20 dB` under dialogue and swells at climax.

### Creative & Editorial Quality
- [ ] **15. Visual Evidence**: Real footage or comparison photos shown before abstract overlays.
- [ ] **16. Continuous Flow**: No awkward clip repeats, freezes, or sudden black frames.
- [ ] **17. Negative Space**: Minimum 0.3s silence before visual scene cuts.
- [ ] **18. Typography Hierarchy**: Headline font (e.g. Clash Display) distinct from UI text (e.g. Satoshi).
- [ ] **19. Micro-Interactions**: Visual actions (clicks, sends, reveals) synchronized with tactile foley.
- [ ] **20. Clear CTA**: Final screen presents an unambiguous action trigger.
- [ ] **21. Deliverable Proofs**: Timestamped snapshot proofs extracted and audited across all scenes.
