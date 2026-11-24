# ⚡ AI Video & Motion Graphics Production Framework

> **A professional, deterministic studio standard for creating AI-powered commercial reels, product films, and kinetic motion graphics.**

---

## 📖 Overview

This repository houses the complete standard operating procedures, architectural blueprints, and production skills for creating high-end, deterministic video compositions. It combines **HyperFrames (HTML/CSS/WebGL-to-video compilation)**, **GSAP timeline animation**, **Edge TTS neural voice synthesis with streaming metadata**, and **ITU-R BS.1770 / EBU R128 broadcast audio mastering**.

---

## 🗂️ Repository Contents

| Component | Path | Description |
| :--- | :--- | :--- |
| **Actionable SOP** | [`video-workflow.md`](video-workflow.md) | The **7-Step Collaborative Pipeline**: Page-by-page narrative budgeting, zero-render layout widgets, clip cue sheets, isolated audio stem auditions, and 0.5s remuxing. |
| **Technical Blueprint** | [`ai-video-editing.md`](ai-video-editing.md) | Universal Production Standard V2.0: EBU R128 mastering math, closed-GOP CFR encoding, Node.js 22+ requirements, and HyperFrames container contracts. |
| **Core Skills** | [`skills/`](skills/) | Specialized production skills for editorial direction, sound design, media handling, and HyperFrames motion components. |

---

## 🛡️ Core Production Philosophy

1. **Strictly Page-by-Page (Screen-by-Screen)**: A video is never treated as an uncontrollable monolithic block. Every scene is an independent atomic page with its own timecode window, DOM viewport container, assigned footage, strict word budget ($\le 2\text{ words/sec}$), and dedicated SFX.
2. **Preview-First, Render-Last**:
   * **Zero-Render UI Inspection**: Layouts, typography, badges, and contrast are reviewed instantly in the browser via an interactive layout widget before rendering any video.
   * **Isolated Stem Audition**: Voiceover and sound effects are reviewed separately before burning into the final mix.
   * **0.5-Second Remuxing**: Visuals and audio are decoupled. Audio changes are remuxed in half a second via FFmpeg stream copy (`-c:v copy -c:a aac`) without waiting for video re-rendering.

---

## 🎛️ Audio Standards

```
Audio Measurement Engine: ITU-R BS.1770 / EBU R128
Social Media Mastering:   -14.0 LUFS Integrated (±0.5 LUFS)
Broadcast TV Target:      -23.0 LUFS Integrated (Cinema / Cable standard)
Maximum True Peak:        -1.0 dBTP (Prevents mobile DAC distortion)
Master Production Audio:  48 kHz, 24-bit PCM WAV
Delivery Format:          AAC Stereo (320 kbps @ 48 kHz)
```

---

## 🛠️ The 5 Core Production Skills

Inside [`skills/`](skills/):
- **`video-editing`**: Master creative direction, visual rhythm, Disney's 12 motion principles, kinetic typography, and editorial pacing.
- **`professional-sound-design`**: Transient-accurate foley editing, silence management, dynamic ducking (music $-20\text{ dB}$ under dialogue), and loudness mastering.
- **`hyperframes`**: Frame-deterministic HTML/CSS rendering contracts, container viewport animations, and GSAP master timelines.
- **`hyperframes-registry`**: 450+ production-ready motion components (kinetic type, charts, glitch overlays, frosted cards, and camera moves).
- **`media-use`**: Footage transcoding rules (Closed-GOP CFR 30fps), color grading, and asset curation.

---

## 🚀 Quickstart

1. Review the Standard Operating Procedure in [`video-workflow.md`](video-workflow.md).
2. Consult [`ai-video-editing.md`](ai-video-editing.md) for FFmpeg encoding parameters, loudnorm commands, and decibel gain calculations.
3. Access modular motion components from [`skills/hyperframes-registry/`](skills/hyperframes-registry/).

---

## 📜 License
MIT License. Created for professional AI video and motion graphics production.
