# 10 — Battery Module (strap-held)

The removable battery lives in a **small 3D-printed module** that sits **under the strap**. The strap holds the module in place against the tracker — no dock, no magnetic connector, no extra hardware. To swap the battery, you unclip the module from under the strap, pop the cell out (JST-PH), and drop in a charged one.

## Why a strap-held module

- **No dock to build or carry** — the module is part of the tracker, not a separate bench item.
- **Tool-free swap** — unclip the module, swap the cell, re-clip. ~10–15 s.
- **No extra connector cost** — the module uses the same **JST-PH 2.0** as the tracker (Rp2.000–5.000).
- **Strap does the retention** — the elastic/leather strap holds the module against the tracker's body; no magnets, no clips, no pogo pins.

## Module design

A small 3D-printed cradle that holds:
- The **pouch cell** (523450: 52×34×5 mm) in a recessed slot with a small lip.
- A **JST-PH 2.0 socket** (cell input) wired to the tracker's TP4056 `B+/B−`.
- A **release tab or clip** so the module unclips from under the strap in one motion.

### Dimensions

| Part | Size (mm) |
|---|---|
| Pouch cell 523450 | 52 × 34 × 5 |
| JST-PH 2.0 socket | ~10 × 8 × 8 |
| Module body (suggested) | ~60 × 40 × 12 (cell + socket + lip) |

### Features

- **Recessed cell slot** with a small lip to hold the cell.
- **JST-PH socket** on the access side, aligned to the cell's plug.
- **Release tab / clip** on the side that tucks under the strap — press to unclip.
- **Alignment guides** (offset pins / keyed slot) so the cell can't be inserted reversed.
- **Strap channel** — a slot or loop where the strap passes over the module, holding it against the tracker.

## How it's held

The module sits **under the strap**, flush against the tracker's body. The strap's tension holds the module in place. No magnets, no screws, no clips — the strap is the retention mechanism.

```
   ┌─────────────────────────┐
   │      [Tracker body]     │
   │                         │
   │   ┌─────────────────┐   │
   │   │  [Battery module]│   │  ← sits under the strap
   │   │  (cell + JST-PH)│   │
   │   └─────────────────┘   │
   └─────────────────────────┘
   ═══════════════════════════  ← strap passes over the module
```

## Swap workflow

1. **Unclip** the module from under the strap (press the release tab).
2. **Pop the dead cell** out (JST-PH unplug).
3. **Drop in a charged cell** (JST-PH plug).
4. **Re-clip** the module under the strap.
5. Done — ~10–15 s.

## Charging the cells

Since there's no dock, charge the spare cells with a **standalone TP4056 charger** (the same module used in the tracker, wired to a USB supply). A simple bench setup:

```
USB (5V) ──→ TP4056 (VIN / GND)
TP4056 (B+ / B−) ──→ JST-PH 2.0 socket
Pouch cell (JST-PH plug) ──→ JST-PH 2.0 socket
```

Or use any **USB LiPo charger** that takes a JST-PH cell. The point: the cells are charged off-tracker, and the charged cells are swapped into the modules as needed.

## Parts

| Part | Notes | ~Price |
|---|---|---|
| JST-PH 2.0 2-pin socket | module's cell input | Rp2.000–5.000 |
| 3D-printed module cradle | sized to the 523450 cell | (print cost) |
| TP4056 (for charging spare cells) | standalone charger | Rp5.000 |
| 5V USB supply | for the standalone charger | Rp20.000–60.000 |

> The module adds **~Rp2.000–5.000** (JST-PH) + print cost per tracker. No dock, no pogo pins, no magnets.

## Safety

- **Only charge cells with PCM** (protection circuit) or via a TP4056 with protection — never a bare, unprotected cell.
- **Don't leave cells charging unattended for hours** — check periodically.
- **Remove a cell that gets hot** during charging immediately.
- The module's **alignment guides** prevent reverse insertion.
