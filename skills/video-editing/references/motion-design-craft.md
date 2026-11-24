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
- **Vector Icon Purity**: Pure inline `<svg>` elements with 1.75px–2.0px stroke lines inside a dedicated 36px–40px frosted glass pill.
- **Layered Frosted Glassmorphism**:
  ```css
  background: rgba(15, 23, 42, 0.65);
  backdrop-filter: blur(24px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.12);
  box-shadow: 0 20px 50px -10px rgba(0, 0, 0, 0.7);
  ```
- **Precision Typography**:
  - Main Headline: `Satoshi` 900 (Black), tight letter-spacing (`-1.5px`).
  - Feature Body: `Google Sans` 700 (Bold) or 500 (Medium).
  - Micro-Tags: `Satoshi` 700, uppercase with positive letter-spacing (`+1.2px`).
- **Polished 2.5D Device Hardware**:
  - Titanium edge reflection (`border: 1px solid rgba(255, 255, 255, 0.15)`).
  - Ambient screen glow casting light onto the 3D background.

---

## 3. Recommended GSAP Easing Presets

```javascript
// High-impact punchy entrances (stamps, badges)
ease: "back.out(1.7)"

// Sleek UI slides (cards, modals)
ease: "power3.out" // or cubic-bezier(0.22, 1, 0.36, 1)

// Smooth camera glides & drone match-cuts
ease: "power2.inOut"
```
