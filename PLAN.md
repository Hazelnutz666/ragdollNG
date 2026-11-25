# Ragdoll Sandbox — Layout & Task Plan

Deliverable: a single `index.html` (HTML + CSS + JS, Matter.js from CDN, Canvas 2D rendering).

---

## 1. UI Layout

```
┌──────────────────────────────────────────────────────────────────────────────┐
│ TOP TOOLBAR                                                                  │
│ [▶/⏸] [⟲ Reset] │ Tool: [Grab][Delete][Explode][Wind][Build] │ Preset: [▼] │ FPS │
├───────────────┬──────────────────────────────────────────────┬───────────────┤
│ LEFT SIDEBAR  │                                              │ RIGHT SIDEBAR │
│ (≈220px)      │                                              │ (≈280px)      │
│               │                                              │               │
│ ▸ Spawn       │                                              │ ▸ Physics     │
│  Ragdoll      │                                              │  Gravity  ──● │
│  Crate        │            SIMULATION VIEWPORT               │  Grav. dir ─● │
│  Metal block  │            (canvas, fills remaining)         │  Time scale ● │
│  Ball (heavy) │                                              │  Air drag  ─● │
│  Wall         │                                              │  Friction  ─● │
│  Platform     │                                              │  Bounce    ─● │
│  Bouncy plat. │                                              │  Joint stiff● │
│  Ramp         │                                              │  [Reset Real.]│
│  Bridge       │                                              │               │
│               │                                              │ ▸ Inspector   │
│ ▸ Characters  │                                              │  (selected)   │
│  list + [x]   │                                              │  Material ▼   │
│               │                                              │  Mass, W, H   │
│ ▸ Environment │                                              │  Friction     │
│  Wind str/dir │                                              │  Bounciness   │
│  Explosion    │                                              │  ☐ Static     │
│   radius/str  │                                              │               │
│  [Clear all]  │                                              │ ▸ Character   │
│               │                                              │  Idle Walk Run│
│               │                                              │  Jump Fall    │
│               │                                              │  Flail Sit    │
│               │                                              │  Dir ◀ ▶      │
├───────────────┴──────────────────────────────────────────────┴───────────────┤
│ STATUS BAR: hint text for current tool · body count · paused state          │
└──────────────────────────────────────────────────────────────────────────────┘
```

- Dark theme via CSS variables; sidebars are collapsible panels.
- Below ~1000px width the sidebars collapse to toggle-able overlays so the viewport stays dominant.
- Spawning: click a spawn button → next click in viewport places it (ghost preview follows cursor). Drag-to-spawn also allowed.

---

## 2. Code Architecture (inside `index.html`)

| Class | Responsibility |
|---|---|
| `PhysicsManager` | Engine, runner loop (fixed timestep), gravity, time scale, boundaries, resize, pause |
| `Ragdoll` | Builds 10 parts (head, torso, 2× upper/lower arm, 2× upper/lower leg), joints with angle limits, collision group |
| `CharacterController` | Per-ragdoll state machine (idle/walk/run/jump/fall/flail/sit) applying forces & torques only |
| `ObjectManager` | `OBJECT_DEFS` registry + `MATERIALS` table; create/remove/update bodies |
| `InteractionManager` | Mouse/touch input, MouseConstraint grabbing, throwing, selection, hover |
| `ToolManager` | Active tool (grab, delete, explode, wind, spawn), tool parameters |
| `PresetManager` | Physics presets (Realistic, Moon, Zero-G, Heavy, Super Bouncy, Low Friction, Chaos) |
| `UIManager` | Builds panels, binds controls ↔ managers, inspector sync |
| `Renderer` | Canvas drawing of bodies, joints, selection, effects (explosion rings, wind particles) |

Extension points: add an entry to `OBJECT_DEFS`, `MATERIALS`, `PHYSICS_PRESETS`, `CHARACTER_STATES` or `TOOLS` — UI is generated from these.

---

## 3. Tasks

### Phase 1 — Foundation
- [x] T1 `index.html` skeleton: layout grid, dark-theme CSS, Matter.js CDN (pinned version)
- [x] T2 `PhysicsManager`: engine, fixed-step loop with `requestAnimationFrame`, pause/play, time scale
- [x] T3 Ground + walls/ceiling boundaries; rebuild on window resize; kill-plane that removes/respawns bodies that escape
- [x] T4 `Renderer`: draw polygons/circles with material colors, constraints, selection outline

### Phase 2 — Objects
- [x] T5 `MATERIALS`: wood, metal, rubber, stone, ice (density, friction, restitution, color)
- [x] T6 `OBJECT_DEFS`: crate, metal block, heavy ball, wall (static/dynamic), platform, bouncy platform, ramp, bridge (chain of planks with constraints)
- [x] T7 `ObjectManager`: spawn at point, remove, clear all, update props (rebuild body when size changes, keep velocity)

### Phase 3 — Ragdolls
- [x] T8 `Ragdoll` construction: parts + pivot constraints, angular limits enforced via corrective torque, self-collision filtering
- [x] T9 Stability: substeps / constraint iterations, max velocity clamp, joint-break guard
- [x] T10 `CharacterController` balance: upright torque on torso/head when "conscious" states active
- [x] T11 States: Idle (balance), Walk/Run (leg-swing torque cycle + horizontal force), Jump (impulse when grounded), Fall (go limp), Flail (random limb torques), Sit (hip/knee target angles)
- [x] T12 Ground detection per ragdoll (collision events on feet) and auto-switch to Fall on large impacts

### Phase 4 — Interaction & Tools
- [x] T13 `InteractionManager`: MouseConstraint grab/drag, throw by release velocity, click-to-select
- [x] T14 Delete tool (object or whole ragdoll)
- [x] T15 Explosion tool: radial impulse with falloff, adjustable radius/strength, visual ring
- [x] T16 Wind tool: global constant force with direction/strength, particle visualization
- [x] T17 Spawn placement mode with ghost preview; Esc to cancel

### Phase 5 — UI & Presets
- [x] T18 Physics sliders bound live to engine (gravity, direction, time scale, air drag, global friction/bounce multipliers, joint stiffness)
- [x] T19 `PresetManager` + preset dropdown + "Reset to Realistic"
- [x] T20 Object inspector: mass, width/height or radius, material, friction, bounciness, static toggle — live
- [x] T21 Character panel: state buttons + facing direction for selected ragdoll; character list in left sidebar
- [x] T22 Reset environment (rebuild default scene), status bar, keyboard shortcuts (Space pause, R reset, 1–5 tools, Del delete)
- [x] T23 Responsive behavior (collapsible sidebars, canvas DPR scaling)

### Phase 6 — Validation
- [x] T24 Headless smoke test (Playwright/Chromium): load page, assert no console errors
- [x] T25 Scripted checks: spawn each object, grab/throw, delete, explode, change preset, edit inspector props, reset, resize
- [x] T26 Stress test: 10 ragdolls + 50 objects, check FPS and no NaN/escaped bodies
- [ ] T27 Manual play-through in desktop browser

---

## 4. Default Scene
Ground, two ragdolls, a small crate stack, a ramp, a bridge between two platforms, and a heavy ball — so every feature is visible on first load.
