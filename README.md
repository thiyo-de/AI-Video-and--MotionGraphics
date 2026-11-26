# ⚡ AI Video & Motion Graphics Production Framework

> **A professional, deterministic studio standard for creating AI-powered commercial reels, product films, and kinetic motion graphics.**

---

## 📖 Overview

This repository houses the complete standard operating procedures, architectural blueprints, and production skills for creating high-end, deterministic video compositions. It combines **HyperFrames (HTML/CSS/WebGL-to-video compilation)**, **GSAP timeline animation**, **Edge TTS neural voice synthesis with streaming metadata**, and **ITU-R BS.1770 / EBU R128 broadcast audio mastering**.

---

## 🗂️ Repository Contents

| Component | Path | Description |
| :--- | :--- | :--- |
| **Actionable SOP** | [`video-workflow.md`](video-workflow.md) | The **9-Stage Hard-Gated Pipeline**: `PLAN.md` (`Gate 1`), zero-render UI preview (`Gate 2`), footage CFR (`Gate 3`), independent `VO`→`SFX`→`BGM`→`Cross-Device WAV Master` (`Gates 4–7`), and 0.5s MP4 remux (`Stage 9`). |
| **Technical Blueprint** | [`ai-video-editing.md`](ai-video-editing.md) | Universal Production Standard V2.0: EBU R128 mastering math, closed-GOP CFR encoding, Node.js 22+ requirements, and HyperFrames container contracts. |
| **Google Flow MCP Guide** | [`flowmcp.md`](flowmcp.md) | Google Flow MCP Integration Guide: CDP automation, session configuration, and Veo/Gemini video generation workflow. |
| **Core Skills** | [`skills/`](skills/) | Specialized production skills for 5-track planning, anti-pattern quality gates, editorial direction, sound design, media handling, and HyperFrames motion components. |
| **Reference Repos** | [`repos/`](repos/) | Cleaned, reusable HTML/GSAP template & motion kits (`herk-edit-kit`, `motion-pack-3`, `product-video-skills`) ready for scene customization. |

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

## 🛠️ The 7 Core Production Skills

Inside [`skills/`](skills/):
- **`planning-video`**: **Stage 1** 5-track pre-production planner (`Flow/Video Clips`, `Motion`, `VO`, `SFX`, `Background Audio`) combining this SOP, the HyperFrames 448-item registry, and `repos/`.
- **`dont-do-in-video-edit`**: Anti-pattern checklist enforcing hard gates (`Gate 1–7`) and preventing PowerPoint slideshows, GSAP flashes/glitches, slider width drift, faint `-22 dBFS` SFX, and untested mixes.
- **`video-editing`**: Master **Stages 1–9** creative direction, visual rhythm, Disney's 12 motion principles, kinetic typography, editorial pacing, and [Reel 03 Production Lessons](skills/video-editing/references/production-lessons-reel03.md).
- **`professional-sound-design`**: Independent Audio Production Pipeline (**Stages 4–8**: `VO` timing lock → `SFX` locked to animation → `BGM` → 5-stem mix → **5-device Cross-Device QA** → **`48 kHz · 24-bit WAV` master** at `-14.0 LUFS / -1.0 dBTP`).
- **`hyperframes`**: Frame-deterministic HTML/CSS rendering contracts, container viewport animations, and GSAP master timelines.
- **`hyperframes-registry`**: 450+ production-ready motion components (kinetic type, charts, glitch overlays, frosted cards, and camera moves).
- **`media-use`**: Footage transcoding rules (Closed-GOP CFR 30fps), color grading, and asset curation.

---

## 📦 Reusable Reference Repositories (`repos/`)

| Repository | What It Adds |
| :--- | :--- |
| [`herk-edit-kit`](repos/herk-edit-kit/) | `MOTION_PHILOSOPHY.md` (11 Laws, perspective grids, light streaks), `406` stylized motion cards (`style-library/`), scene templates, and transcript-driven editing skills. |
| [`motion-pack-3`](repos/motion-pack-3/) | `10` standalone `1080×1920 @ 30fps` vertical templates (audio waveform, iMessage stack, Apple Maps route, toggle flip, stat counters, progress steps). |
| [`product-video-skills`](repos/product-video-skills/) | Modular `pv.js` / `pv.css` GSAP motion engine (velocity-matched cuts, 3D `PV.plane`, `PV.crop`, auto-sizing `PV.cycle` pills) and beat-grid tools. |

---

## 🚀 Quickstart (`Stage 1 → Stage 9`, Gate-by-Gate)

1. **Stage 1 (`planning-video`)**: Lock a 5-track `PLAN.md` across clips, motion, VO, SFX, and background music (**🛑 Gate 1**).
2. **Stages 2–3**: Build interactive `layout_preview_widget.html` (**🛑 Gate 2**), then prep CFR clips/Flow (**🛑 Gate 3**).
3. **Stages 4–8 (Independent Audio Pipeline)**: Generate & approve `VO` (**🛑 Gate 4** → locks cut frames) → `SFX` locked to animation (**🛑 Gate 5**) → `BGM` (**🛑 Gate 6**) → 5-Stem Mix & **5-Device Cross-Device QA** → **Approved `48 kHz · 24-bit WAV` Master** (**🛑 Gate 7**).
4. **Stage 9**: Render headless with HyperFrames (`-q looks`), 0.5s mux (`-c:v copy`), audit the delivered MP4, and ship.

---

## 📜 License
MIT License. Created for professional AI video and motion graphics production.
