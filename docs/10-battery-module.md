# 10 — Battery (direct solder, not hot-swappable)

The battery is a **small LiPo (~34×25×5 mm, the size of the D1 Mini)** with wires **soldered directly** to the battery shield's B+/B− pads. There is **no JST-PH connector** — the battery is a permanent part of the build, not hot-swappable.

## Why direct solder (design change)

The original design used a 523450 (52×34×5 mm) with a JST-PH hot-swap connector. That was replaced because:
- The 523450 was **too large** for the compact build.
- The small LiPo (~34×25×5 mm) fits **alongside the D1 Mini + shield stack**, keeping the build compact.
- Soldering the wires directly **saves space** (no JST-PH connector needed) and simplifies the wiring.

**Trade-off:** the battery is no longer hot-swappable. To replace the battery, desolder the wires and solder in a new cell.

## Battery connection

```
Small LiPo (+) ──[soldered directly]──→ battery shield B+
Small LiPo (−) ──[soldered directly]──→ battery shield B−
```

- The small LiPo's wires are **soldered directly** to the shield's B+/B− pads.
- **No JST-PH connector** — the battery is a permanent part of the build.
- The small LiPo (~34×25×5 mm) fits alongside the D1 Mini + shield stack.

## Replacing the battery

1. **Desolder** the two wires from the shield's B+/B− pads.
2. **Solder** the new cell's wires to the same pads.
3. **Verify** the battery voltage (3.7–4.2V) and the 5V output.

## Charging the cells

Since the battery is not hot-swappable, charge the tracker **in-situ** via the USB micro port on the battery shield:

```
USB (5V) ──→ battery shield VIN ──→ charges the battery
```

Or desolder the battery and charge it with a standalone TP4056 charger, then re-solder it.

## Parts

| Part | Notes | ~Price |
|---|---|---|
| Small LiPo (~34×25×5 mm) | search Tokopedia: "baterai lipo kecil 3.7v" | Rp20.000–40.000 |
| Hook-up wire (for the battery leads) | 22–26 AWG | Rp5.000 (roll) |

> The battery is a permanent part of the build. No JST-PH connector, no hot-swap module.

## Safety

- **Only charge cells with PCM** (protection circuit) or via a TP4056 with protection — never a bare, unprotected cell.
- **Don't leave cells charging unattended for hours** — check periodically.
- **Remove a cell that gets hot** during charging immediately.
- The direct-solder connection is permanent — no risk of the connector vibrating loose.
