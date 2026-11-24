# Surgical Sound Design & EBU R128 Audio Mastering

## 1. The Core Philosophy
Sound design is **acoustic punctuation**. It gives weight, mass, and texture to visual changes.
If an animation lasts 250 milliseconds, the sound effect must NOT linger for 2.5 seconds.

---

## 2. Micro-Trimming & Duration Caps

Before any sound effect enters the timeline, pre-process it through Librosa/FFmpeg:
1. Strip leading silence so the transient strike arrives at **0.00ms latency**.
2. Strip trailing reverb decay tails that clutter subsequent scenes.
3. Apply 8ms–12ms micro-fades at the start and end to eliminate digital boundary clicks.

| Sound Category | Visual Correlate | Maximum Allowed Duration | Target Gain |
| :--- | :--- | :---: | :---: |
| **UI Click / Tap** | Hotspot radar pulse / Button tap | **40ms – 120ms** | 0.40 – 0.55 |
| **Feature Pop / Reveal** | Card glide / Badge entrance | **60ms – 180ms** | 0.45 – 0.60 |
| **Spatial Whoosh** | Match-cut / Camera sweep | **180ms – 280ms** | 0.60 – 0.75 |
| **Impact / Rejection Slam** | Rubber stamp / Harsh cancel | **100ms – 220ms** | 0.65 – 0.80 |
| **Prestige Outro Hit** | Final logo resolution | **250ms – 400ms** | 0.75 – 0.85 |

---

## 3. Negative Space & Overlap Standards
- **Minimum Negative Space**: Keep at least **1.5s to 3.0s of intentional silence** between SFX cues.
- **Total Active SFX Budget**: In a 30-second commercial video, total active sound effect duration across all cues combined must be **less than 1.2 seconds**.
- The remaining time belongs exclusively to clear voiceover narration and ducked background music.

---

## 4. Broadcast EBU R128 Loudness Standards

Always execute two-pass linear loudness normalization via FFmpeg `loudnorm`:

```bash
# Pass 1: Measure
ffmpeg -i rough_mix.wav -af loudnorm=I=-14:TP=-1.0:LRA=7:print_format=json -f null -

# Pass 2: Linear Apply
ffmpeg -i rough_mix.wav -af loudnorm=I=-14.0:TP=-1.0:LRA=7.0:measured_I=...:measured_TP=...:measured_LRA=...:measured_thresh=...:offset=...:linear=true -ar 48000 -c:a pcm_s24le master_audio.wav
```

### Target Specifications:
- **Integrated Loudness**: **−14.0 LUFS (±0.5 LUFS)**
- **Loudness Range (LRA)**: **≤ 7.0 LU**
- **True Peak Ceiling**: **−1.0 dBTP**
- **Sampling Rate**: **48,000 Hz Stereo**
