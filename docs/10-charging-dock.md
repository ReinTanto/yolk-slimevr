# 10 — Charging Dock

Because the battery is **hot-swappable (removable)**, the cleanest way to recharge is a **charging dock**: a small 3D-printed cradle that holds a bare pouch cell and charges it via a TP4056 module. You pop a dead cell out of the tracker, drop it in the dock, and it charges on the bench — no need to open the tracker case or wire a charger into each tracker.

## Why a dock (vs. charging the tracker in-situ)

- **No USB port needed in the tracker case** — the tracker case stays sealed and smaller.
- **One charger for all 5 cells** — a single dock (or a 5-slot bank) charges any cell.
- **Faster turnaround** — swap a charged cell in 5–10 s; the dead one charges in the dock.
- **Less soldering** — the dock is a standalone, simple circuit.

## Dock circuit

```
USB (5V, USB-A or USB-C) ──→ TP4056 (VIN / GND)
TP4056 (B+ / B−) ──────────→ JST-PH 2.0 socket (cell input)
Pouch cell (JST-PH plug) ───→ JST-PH 2.0 socket
```

That's it. The TP4056 (with protection) charges the cell CC/CV to 4.2V and protects it (over-discharge / over-current / short). **No MT3608 step-up in the dock** — the dock only charges the cell; it doesn't power the tracker.

| Part | Qty | Notes |
|---|---|---|
| TP4056 module (Type-C, with protection) | 1 per slot | same as the tracker's charger |
| JST-PH 2.0 2-pin socket | 1 per slot | cell input |
| USB power (5V) | 1 | USB-A wall adapter or USB-C; use a **data/5V** supply |
| Status LED (optional) | 1 per slot | TP4056 has built-in charge/full LEDs — usually no extra part needed |
| 3D-printed cradle | 1 per slot | sized to the 523450 cell (52×34×5 mm) |

## 5-slot dock (recommended)

Print a **5-slot bank**: five TP4056 modules, each with a JST-PH socket and a cell cradle, all fed from one USB hub or a 5V multi-port adapter. One cable charges all five spare cells at once.

- **Power budget:** a 1A TP4056 per slot → up to 5A total. Use a **5V 5–10A** supply (a quality USB-C PD adapter or a multi-port 5V adapter). If the supply is undersized, the cells charge slower (CC current is shared) — not dangerous, just slower.
- **Stagger the load:** you rarely charge all 5 at once; a 5V 5A supply is plenty.

## Dock design (3D-printed cradle)

- **Cell cradle:** a recessed tray sized to the 523450 cell (52×34×5 mm) with a small lip so the cell sits flat and the JST-PH plug mates the socket.
- **JST-PH socket** mounted on the cradle's access side, aligned to the cell's plug.
- **TP4056** mounted flat, `B+/B−` to the socket, `VIN/GND` to the USB supply.
- **LED window** over the TP4056's charge/full LEDs so you can see status without opening the dock.
- **Alignment guides** so the cell can't be inserted reversed (offset pins / keyed slot).
- **Label each slot** (or color-code) so you know which cell is which.

## Charging workflow

1. Pop the **dead cell** out of the tracker (JST-PH unplug).
2. Drop it into a **dock slot** (JST-PH plug into the socket).
3. The dock's **TP4056** charges it to 4.2V (red LED = charging, blue/green = full).
4. When full, **swap a charged cell** into the tracker.
5. Repeat — keep a **bank of charged spares** so a session never runs out.

## Safety

- **Only charge cells with PCM** (protection circuit) or the TP4056's protection — never a bare, unprotected cell.
- **Don't leave unattended for hours** — check the dock periodically; a failing cell can overheat.
- **Charge in a ventilated area**, away from flammables.
- **Remove a cell that gets hot** during charging immediately.
- The TP4056's over-current protection cuts the cell at ~3A; the cell's PCM (if present) adds a second layer.

## Parts (Tokopedia)

| Part | Link | ~Price |
|---|---|---|
| TP4056 Type-C (with protection) | [TP4056 Type-C (Mirorim)](https://www.tokopedia.com/mirorim/tp4056-type-c-18650-battery-charging-module-lithium-ion-protection) | Rp5.000 |
| JST-PH 2.0 2-pin socket | search Tokopedia: "konektor JST PH 2.0 2 pin" | Rp2.000–5.000 |
| 5V USB supply (5–10A) | search Tokopedia: "adaptor usb 5v 5a" / "charger usb c pd 65w" | Rp20.000–60.000 |

> A 5-slot dock ≈ 5× TP4056 + 5× JST-PH + 1× 5V supply + printed cradles ≈ **Rp50.000–100.000** one-time, then it recharges every cell forever.
