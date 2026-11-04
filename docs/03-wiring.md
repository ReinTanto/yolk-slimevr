# 03 — Wiring

> **Visual:** see the Draw.io wiring diagram — [`diagrams/wiring-diagram.drawio`](../diagrams/wiring-diagram.drawio) (open in [draw.io](https://app.diagrams.net) or the VS Code Draw.io Integration extension).

## Power chain (per tracker)

**Chosen: D1 Mini battery shield + TP4056/MT3608 charger (soldered on top) + toggle switch**

```
Small LiPo (+) ──[soldered directly]──→ battery shield B+
Small LiPo (−) ──[soldered directly]──→ battery shield B−
USB micro (VCC) ─────────────→ battery shield VIN
USB micro (GND) ─────────────→ battery shield GND

Battery shield 5V ────────────→ D1 Mini 5V pin
Battery shield GND ──[toggle switch]──→ D1 Mini GND

Charger (TP4056/MT3608) ──[pins]──→ D1 Mini top pads (5V, GND, VIN)
IMU (GY-LSM6DS3) ──[copper enamel wire]──→ D1 Mini backside (3V3, GND, SDA, SCL)
```

The **battery shield** is the same W×L as the D1 Mini but thicker (a 5 mm tall coil on the board). The **battery** is a small LiPo (~34×25×5 mm, the size of the D1 Mini) with wires **soldered directly** to the shield's B+/B− pads (no JST-PH connector). The **charger** (TP4056/MT3608) is soldered via pins to the top of the D1 Mini. The **IMU** (GY-LSM6DS3) is soldered with copper enamel wire and hot-glued to the backside of the D1 Mini. A **toggle switch** (SPST) is in series with GND.

> **Do not** power the D1 Mini directly from the 3.7V cell — it needs 5V. The step-up (on the charger) is mandatory.
> **Set the output to 5.0V** (measure with a multimeter) before connecting the load.

### Why the battery shield (design change)

The original TP4056/MT3608 combined board (Supreme ID) was replaced because:
1. **It had issues** (unreliable).
2. **It was slightly larger** than the D1 Mini.

The battery shield is the same W×L as the D1 Mini, but thicker (5 mm coil). The charger is now a separate module soldered on top. See the [design change log](02-parts-list.md#design-change-log) for details.

## I²C — GY-LSM6DS3 → ESP8266

| GY-LSM6DS3 | ESP8266 (NodeMCU / D1-Mini-style) |
|---|---|
| VCC | 3V3 |
| GND | GND |
| SDA | D2 (GPIO4) |
| SCL | D1 (GPIO5) |
| SDO/SA0 | GND → I²C address **0x6A** (or VCC → **0x69**) |

> The Kyware board is NodeMCU-style, so it uses the same **D0–D8** pin labels as a D1 Mini. **Confirm the silkscreen on your exact board** and map to the real GPIOs. If your board labels differ, set the actual GPIO numbers in `defines.h` (see [04-firmware.md](04-firmware.md)).
> A single IMU usually works without external I²C pull-ups. If you add more I²C devices later, add 4.7kΩ pull-ups on SDA and SCL.

## Battery connection (direct solder, no connector)

- The small LiPo's wires are **soldered directly** to the battery shield's B+ / B− pads.
- **No JST-PH connector** — the battery is a permanent part of the build (not hot-swappable).
- To replace the battery, desolder the wires and solder in a new cell.
- The small LiPo (~34×25×5 mm) fits alongside the D1 Mini + shield stack, keeping the build compact.

## Full netlist (per tracker) — battery shield build

| From | To |
|---|---|
| Small LiPo + [soldered directly] | battery shield B+ |
| Small LiPo − [soldered directly] | battery shield B− |
| USB micro VCC | battery shield VIN |
| USB micro GND | battery shield GND |
| battery shield 5V | D1 Mini 5V pin |
| battery shield GND → [toggle switch] | D1 Mini GND |
| charger (TP4056/MT3608) 5V [via pins] | D1 Mini 5V pad (top) |
| charger (TP4056/MT3608) GND [via pins] | D1 Mini GND pad (top) |
| D1 Mini 3V3 [copper enamel wire] | GY-LSM6DS3 VCC (backside) |
| D1 Mini GND [copper enamel wire] | GY-LSM6DS3 GND (backside) |
| D1 Mini D2 (GPIO4) [copper enamel wire] | GY-LSM6DS3 SDA (backside) |
| D1 Mini D1 (GPIO5) [copper enamel wire] | GY-LSM6DS3 SCL (backside) |
| Toggle switch (SPST) | in series with GND (shield GND → D1 Mini GND) |

## Battery module (strap-held)

The removable battery lives in a **small 3D-printed module** that sits **under the strap**. The strap holds the module in place — no dock, no magnetic connector. To swap the battery, unclip the module, pop the cell out (JST-PH), and drop in a charged one. Spare cells are charged off-tracker with a standalone TP4056. Full design, workflow, and safety: see [10-battery-module.md](10-battery-module.md).

## Optional

- **Battery voltage divider** → ESP8266 A0 (ADC), for battery % in the SlimeVR server.
- **Schottky diode** (1N5819) between TP4056 BAT+ and MT3608 VIN+ to prevent backflow when powering from USB while the cell is connected.
- **LED:** the ESP8266's onboard LED (D4 / GPIO2 on D1-Mini-style) shows status — no extra part needed.
