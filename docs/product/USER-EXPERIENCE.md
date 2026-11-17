# User Experience & Design Philosophy — Sagar OS

> **Visual language, interaction paradigms, and ergonomics of Sagar OS.**

---

## 1. Visual Design Language

Sagar OS embraces a minimal, high-contrast, and typography-first visual identity.

### 1.1 Aesthetic Principles
- **No Skeuomorphic Gradients or Excessive Blur:** Clean geometric surfaces with subtle depth and clear window borders.
- **High-Legibility Typography:** Clean sans-serif system fonts with carefully balanced weight hierarchy and font-hinting tailored for high-DPI and standard displays.
- **First-Class Dark and Light Modes:** System-wide dark and light themes that propagate automatically across all first-party apps and compliant third-party toolkits via the freedesktop dark-mode portal.

### 1.2 Color Palette & Contrast
- High contrast ratios (WCAG AAA compliance for core UI text).
- Neutral slate/zinc grays for window backgrounds to reduce eye strain.
- A single, cohesive accent color palette used intentionally to highlight focused elements without visual cacophony.

---

## 2. Interaction & Navigation Paradigm

### 2.1 Keyboard-First Ergonomics
While Sagar OS provides full mouse and multi-touch gesture support, every system interaction can be executed without leaving the keyboard:

| Action | Interaction Pattern |
| :--- | :--- |
| **Launch Application** | `Super` key opens launcher; type 2-3 letters + `Enter` |
| **Switch Workspace** | `Super + 1..9` or `Super + Left/Right` |
| **Window Snapping** | `Super + Arrow Keys` (half-screen, quadrant tiling) |
| **System Settings** | `Super + ,` opens Sagar Settings |
| **Lock Screen** | `Super + L` locks immediately |
| **Open Terminal** | `Super + Enter` launches primary terminal instance |

### 2.2 Window Management Model
- **Dynamic Floating with Smart Tiling:** Windows open centered and appropriately sized by default, but can be seamlessly snapped into 50/50 splits or 25% quadrants with intuitive keyboard shortcuts or edge drag.
- **Predictable Window Focus:** Clear active window borders (no ambiguous active window states).

### 2.3 Gesture Navigation
- Three-finger horizontal swipe switches virtual workspaces.
- Three-finger vertical swipe opens the workspace overview and active window grid.
- Pinch-to-zoom support across document viewers and web surfaces.

---

## 3. Notification & Interruption Discipline

- **No Stealing Focus:** Applications cannot grab keyboard or mouse focus without explicit user interaction.
- **Focus Modes ("Do Not Disturb"):** One-click toggle disables all notifications and visual badges during meetings, deep work, or presentations.
- **Actionable Toasts:** Notifications appear in a dedicated, unobtrusive screen corner with clear primary action buttons (e.g., "Reply", "Dismiss", "Open").
