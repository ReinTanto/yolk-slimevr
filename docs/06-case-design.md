# 06 — Case Design (3D-printed)

The case is designed from scratch in a CAD package (Fusion 360 / FreeCAD / SolidWorks) around the chosen parts. One design per tracker type (chest vs. wrist/ankle can differ in strap + size).

## Key part dimensions to design around

| Part | Dimensions (mm) |
|---|---|
| Kyware ESP8266 (NodeMCU-style) | ~70 × 35 × 15 (confirm on the board) |
| GY-BMI160 / Mumo module | Mumo: ~25 × 18 × 3 (1.2 mm PCB, castellated); GY-BMI160: ~20 × 20 × 3 |
| Pouch cell 523450 (chosen, 1000 mAh) | 52 × 34 × 5 (L×W×T) |
| Pouch cell 523450 (alt, 1500 mAh) | 52 × 34 × 5 (L×W×T) |
| Pouch cell PALO 103450 (alt, 2000 mAh) | 10 × 34 × 50 |
| TP4056 module | ~27 × 17 × 3 |
| MT3608 module | ~20 × 12 × 5 (with trim pot) |
| JST-PH 2.0 socket | ~10 × 8 × 8 |
| Slide switch (SPST) | 6 × 3 × 12 |
| USB Type-C port | ~9 × 7 (through-hole) |

## Required features

| Feature | Why |
|---|---|
| **MCU pocket** | snug fit, 0.2 mm clearance per side |
| **IMU mount** | flat, secure; Mumo has castellated edges for soldering |
| **Battery bay (hot-swap)** | recessed slot for the pouch cell + JST-PH socket access |
| **JST-PH retaining clip + alignment guides** | so the connector can't vibrate loose or insert reversed |
| **USB Type-C cutout** | charging without opening the case; use a snap-fit or screw-down port |
| **Switch slot** | on the side wall, 6 × 3 mm |
| **Strap mount** | loop/slot for a ~25 mm elastic or leather strap |
| **Reset access** | 2 mm hole aligned with the RST button (pin-pressable) |
| **LED window** | small hole over the status LED |
| **Ventilation** | 3–4 × 2 mm holes (ESP8266 + MT3608 get warm) |

## Hot-swap battery bay

- **Recessed slot** sized to the pouch cell (523450: 52×34×5 mm) with a small lip to hold it.
- **JST-PH 2.0 socket** soldered to the board, positioned so the cell's plug mates from the access side.
- **Retaining clip** (printed catch or a small metal clip) holds the plug.
- **Alignment guides** (offset pins or a keyed slot) prevent reverse insertion.
- **Access door** (hinged or snap) so a cell can be swapped in ~5–10 s without tools.

## Printing tips

- **Material:** PLA is fine; **PETG** is tougher and more heat-resistant (better for the warm MT3608/ESP8266).
- **0.2 mm layer height**, **20–30% infill**, 3–4 wall perimeters.
- **Tight MCU fit:** 0.2 mm clearance per side. Too loose = rattle; too tight = won't insert.
- **USB port:** print a **snap-fit USB-C insert** or use a **screw-down port** — a poorly fitted port is the #1 charging failure in DIY builds.
- **Two-tone print** (black body + colored accent) helps identify trackers (chest / L-wrist / R-wrist / L-ankle / R-ankle).
- **Print an empty case first** and verify the MCU, IMU, battery, TP4056, MT3608, switch, and USB port all fit before committing.

## Suggested internal layout (top-down)

```
┌──────────────────────────────────────────┐
│  [Kyware ESP8266]                        │
│                                         │
│  [Mumo ICM-45686]   [TP4056] [MT3608]   │
│                                         │
│  [Pouch cell bay (hot-swap, JST-PH)]    │
│  ─────────────────────────────────────   │
│  [Switch]  [USB-C]  (side wall)         │
│  [Strap mount] (back)                   │
└──────────────────────────────────────────┘
```

## Mumo module note

The [SlimeVR Mumo Breakout Module V1.1](https://shop.slimevr.dev/products/slimevr-mumo-breakout-module-v1-icm-45686-qmc6309) ships with a published **schematic** and **STEP file** for the case — use the STEP file to model the exact footprint. PCB is 1.2 mm thick with castellated edges (easier soldering). Pin header not included.

## Charging dock (separate print)

The removable cells are recharged in a **charging dock** — a separate 3D-printed cradle (not part of the tracker case). Each slot holds a bare 523450 cell (52×34×5 mm) and a TP4056 module, with a JST-PH socket and an LED window. Print a **5-slot bank** fed from one 5V 5–10A supply. Design, layout, and workflow: see [10-charging-dock.md](10-charging-dock.md).
