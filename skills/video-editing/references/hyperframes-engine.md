# HyperFrames & FFmpeg Execution Engine

## 1. Composition Contract (`index.html`)

The root container must declare explicit canvas dimensions and framerate:
```html
<div
  id="root"
  data-composition-id="main"
  data-start="0"
  data-duration="30.00"
  data-width="1080"
  data-height="1920"
  data-fps="30"
>
```

---

## 2. Video & Audio Tag Rules

1. **Embedded Video Clips**:
   - Silent video footage MUST use: `muted playsinline`.
   - ❌ **Prohibited**: Do NOT use `autoplay loop` on multiple video elements. In headless Chrome, simultaneous autoplay loops overwhelm internal socket range requests, resulting in `net::ERR_CONNECTION_REFUSED`.
   - Always declare `data-start` and `data-duration` on every media element.
2. **Audio Elements**:
   - Master voice: `data-start="0" data-duration="..."`
   - Micro-SFX cues: Pre-loaded with exact `data-start` matching the GSAP keyframe triggers.
3. **Layout Audits**:
   - Add `data-layout-ignore` to texture text, HUD decorations, and watermarks under 28px floor height to keep linter checks 100% clean.

---

## 3. Standard Verification & Render Commands

```powershell
# 1. Verification Check (Lint, Layout, Motion, Audio, Contrast)
$env:HYPERFRAMES_FFMPEG_PATH=(Get-Command ffmpeg -CommandType Application).Source
$env:HYPERFRAMES_FFPROBE_PATH=(Get-Command ffprobe -CommandType Application).Source
npx hyperframes check /path/to/project

# 2. Headless GPU-Accelerated Render
npx hyperframes render /path/to/project -o /path/to/output_raw.mp4 -q looks --format mp4

# 3. Master Multiplexing with -14 LUFS Audio
ffmpeg -y -i output_raw.mp4 -i master_audio_ebur128.wav -map 0:v:0 -map 1:a:0 -c:v copy -c:a aac -b:a 320k -shortest final_master.mp4
```
