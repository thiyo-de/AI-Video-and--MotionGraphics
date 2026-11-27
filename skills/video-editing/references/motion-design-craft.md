# Motion Design Craft & Animation Principles

## 1. Disney's 12 Animation Principles Adapted to UI

| Principle | Traditional Meaning | Modern Motion Graphics Execution |
| :--- | :--- | :--- |
| **1. Anticipation** | Winding up before a jump | Subtle reverse motion (-4% scale or -15px translation) before rapid acceleration |
| **2. Staging** | Directing viewer focus | One primary motion event at a time; secondary elements wait 0.1s – 0.2s |
| **3. Follow-Through & Overlap** | Inertia when stopping | The card arrives first; the vector icon settles 0.08s later; badge glows on rest |
| **4. Slow In & Slow Out** | Non-linear acceleration | Physics cubic-bezier curves (`0.22, 1, 0.36, 1`) rather than flat linear eases |
| **5. Secondary Action** | Supporting movements | Glowing edge sweep, subtle 360° gyro rotation, or ambient particle float |

---

## 2. Eliminating "AI Slop" in Video UI

### ❌ The Amateur Markers:
- Raw Unicode emojis (`🏛️`, `🔬`, `📚`, `📲`, `❌`) rendering in flat Segoe UI Emoji fonts.
- Flat solid cards with loud 4px neon borders.
- Centered bullet lists stacked inside a plain dark box.
- Generic mobile phone frames with blocky black borders.

### ✅ The Senior Motion Designer Standards:
- **Vector Icon Purity**: Pure inline `<svg>` elements with 1.75px–2.0px stroke lines (no emojis).
- **Brief-Driven Surface Choice (Plateless Scrims OR Frosted Bento)**: Use edge-to-edge footage + unboxed *"type without plates"* over subtle gradient scrims (`.scrim`) when visuals carry the space, OR layered translucent cards where structured UI/video choreography demands framing:
  ```css
  background: rgba(15, 23, 42, 0.65);
  backdrop-filter: blur(24px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.12);
  box-shadow: 0 20px 50px -10px rgba(0, 0, 0, 0.7);
  border-radius: 24px;
  ```
- **Brief-Matched Typography (Zero Unsolicited Italics)**: Adapt display, body, and technical mono pairings to the domain (e.g., `Satoshi`/`Google Sans`, editorial architectural grotesk, `JetBrains Mono` with `tabular-nums`), maintaining tight display tracking and high contrast.
- **Polished 2.5D Device Hardware**:
  - Titanium edge reflection (`border: 1px solid rgba(255, 255, 255, 0.15)`).
  - Ambient screen glow casting light onto the 3D background.

---

## 3. Creative Transition & VO-Card Video Patterns (`f(time)` Safe)
- **Deterministic Foreground & Optical Wipes**: Animate subtle matte masks, directional light curtains, or brief-appropriate foreground sweeps purely via timeline transforms (`xPercent`, `yPercent`, `scale`, `opacity`), never `Math.random()` or CSS keyframes. Sync scene swap to max occlusion frame.
- **Cinematic Component Focus-Zoom**: Set `transformOrigin` on the card/component wrapper (`#target-card`), apply 5% anticipation pull followed by exponential GPU scale-through (`scale: 1 -> 3.0+`, `ease: "power4.in"`) into continuous `data-media-start` fullscreen footage. Never stack full-viewport CSS `blur()` over `backdrop-filter`.
- **VO-Synced Clips Inside Cards**: Pre-render all cards with explicit `t=0` `.set(...)` baselines, pre-prime `<video muted playsinline preload="auto">` at Frame 0, and trigger each card's active highlight + video motion at exact `Stage 4` `WordBoundary` phrase times (`never .add() DOM mutations`).

---

## 4. Recommended GSAP Easing Presets

```javascript
// High-impact punchy entrances (stamps, badges)
ease: "back.out(1.7)"

// Sleek UI slides (cards, modals)
ease: "power3.out" // or cubic-bezier(0.22, 1, 0.36, 1)

// Smooth camera glides & drone match-cuts
ease: "power2.inOut"
```
