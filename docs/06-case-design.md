# 06 — Case Design (3D-printed)

The case is designed from scratch in a CAD package (Fusion 360 / FreeCAD / SolidWorks) around the chosen parts. One design per tracker type (chest vs. wrist/ankle can differ in strap + size).

> **Visuals:** see the Draw.io layout diagrams — [`diagrams/tracker-layout.drawio`](../diagrams/tracker-layout.drawio) (top-down component placement) and [`diagrams/case-layout.drawio`](../diagrams/case-layout.drawio) (stacked case, top-down + side view). Open in [draw.io](https://app.diagrams.net) or the VS Code Draw.io Integration extension.
>
> **CAD renders:**
> - [`media/3d case isometric top view linework.png`](../media/3d%20case%20isometric%20top%20view%20linework.png) — top-down linework
> - [`media/3d case Isometric view above.png`](../media/3d%20case%20Isometric%20view%20above.png) — isometric view from above
> - [`media/3d case bottom isometric view.png`](../media/3d%20case%20bottom%20isometric%20view.png) — bottom isometric view
> - [`media/3d case bottom view, interior.png`](../media/3d%20case%20bottom%20view%2C%20interior.png) — bottom view, interior layout

## Key part dimensions to design around

| Part | Dimensions (mm) |
|---|---|
| Wemos D1 Mini (ESP8266) | 34.2 × 25.6 × ~3 |
| D1 Mini battery shield | Same W×L as D1 Mini (34.2 × 25.6), thick (~8–10 mm with the 5 mm coil) |
| GY-LSM6DS3 | ~20 × 20 × 3 (soldered on the backside of the D1 Mini) |
| Small LiPo (built-in, D1 Mini size) | ~34 × 25 × 5 (L×W×T), wires soldered directly to the shield |
| Toggle switch (SPST) | ~10 × 5 × 15 |
| USB micro port (on the shield) | ~8 × 7 (through-hole) |
| USB Type-C port (on the D1 Mini) | ~8 × 7 (through-hole) |

## Stacked layout (top → bottom)

| Layer | Part | Notes |
|---|---|---|
| **TOP** | Battery Shield (TP4056 + 5 mm coil) | Soldered directly onto the D1 Mini; USB micro (charging) on this layer |
| **MIDDLE** | D1 Mini + GY-LSM6DS3 (soldered on backside) | USB Type-C (flashing) on this layer |
| **BOTTOM** | Built-in LiPo (2000 mAh, D1 Mini size) | Skin-facing; wires soldered directly to shield B+/B− |

The **toggle switch** sits between the D1 GND and Shield GND, **offset on the short side** of the PCB, accessible from outside the case.

## Required features

| Feature | Why |
|---|---|
| **Shield pocket** | snug fit, 0.2 mm clearance per side |
| **D1 Mini pocket** | snug fit, 0.2 mm clearance per side |
| **IMU mount** | flat, secure; soldered on the backside of the D1 Mini |
| **Battery bay (built-in)** | recessed slot for the LiPo (34×25×5 mm); wires soldered directly — no JST-PH |
| **USB micro cutout** | charging without opening the case; snap-fit or screw-down port |
| **USB Type-C cutout** | flashing without opening the case; snap-fit or screw-down port |
| **Switch slot** | on the short side wall, 6 × 3 mm, accessible from outside |
| **Strap mount** | loop/slot for a ~25 mm elastic or leather strap |
| **Reset access** | 2 mm hole aligned with the RST button (pin-pressable) |
| **LED window** | small hole over the status LED |
| **Ventilation** | 3–4 × 2 mm holes (ESP8266 + TP4056 get warm) |

## Printing tips

- **Material:** PLA is fine; **PETG** is tougher and more heat-resistant (better for the warm TP4056/ESP8266).
- **0.2 mm layer height**, **20–30% infill**, 3–4 wall perimeters.
- **Tight fit:** 0.2 mm clearance per side on the D1 Mini and shield. Too loose = rattle; too tight = won't insert.
- **USB ports:** print a **snap-fit USB insert** or use a **screw-down port** — a poorly fitted port is the #1 charging failure in DIY builds.
- **Two-tone print** (black body + colored accent) helps identify trackers (chest / L-wrist / R-wrist / L-ankle / R-ankle).
- **Print an empty case first** and verify the shield, D1 Mini, IMU, battery, switch, and both USB ports all fit before committing.

## Suggested internal layout (top-down, looking at the shield)

```
┌────────────────────────────────────┐
│  [USB micro (charging)]           │
│                                   │
│  [Battery Shield (TP4056)]        │
│                                   │
│  [USB Type-C (flashing)]     [Sw] │
│                                   │
└────────────────────────────────────┘
   ~38 mm × ~29 mm (D1 Mini footprint + margin)
```

The **toggle switch** is offset on the short side (right edge in the diagram). All layers are stacked; the battery is skin-facing (bottom).

## Mumo module note

The [SlimeVR Mumo Breakout Module V1.1](https://shop.slimevr.dev/products/slimevr-mumo-breakout-module-v1-icm-45686-qmc6309) ships with a published **schematic** and **STEP file** for the case — use the STEP file to model the exact footprint. PCB is 1.2 mm thick with castellated edges (easier soldering). Pin header not included.
