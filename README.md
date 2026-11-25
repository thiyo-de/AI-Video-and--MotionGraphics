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
- **`planning-video`**: 5-track pre-production planner (`Flow/Video Clips`, `Motion`, `VO`, `SFX`, `Background Audio`) combining this SOP, the HyperFrames 448-item registry, and `repos/`.
- **`dont-do-in-video-edit`**: Anti-pattern checklist preventing PowerPoint slideshows/transitions, GSAP `.add()`/repeat glitches, slider width drift, faint UI clicks, and stale captures.
- **`video-editing`**: Master creative direction, visual rhythm, Disney's 12 motion principles, kinetic typography, editorial pacing, and [Reel 03 Production Lessons](skills/video-editing/references/production-lessons-reel03.md).
- **`professional-sound-design`**: Peak-anchored slicing (`np.argmax`), audible mobile RMS staging, separate 3-bucket cues, dynamic ducking, and EBU R128 mastering (`-14.0 LUFS / -1.0 dBTP`).
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

## 🚀 Quickstart

1. Run **`planning-video`** (`skills/planning-video/SKILL.md`) to lock a 5-track `PLAN.md` across clips, motion, VO, SFX, and background music before rendering.
2. Review the **7-Step SOP** in [`video-workflow.md`](video-workflow.md) and FFmpeg mastering formulas in [`ai-video-editing.md`](ai-video-editing.md).
3. Pull components from [`skills/hyperframes-registry/`](skills/hyperframes-registry/) or [`repos/`](repos/), and audit every scene against [`skills/dont-do-in-video-edit/`](skills/dont-do-in-video-edit/SKILL.md).

---

## 📜 License
MIT License. Created for professional AI video and motion graphics production.
