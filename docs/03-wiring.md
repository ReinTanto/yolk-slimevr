# 03 — Wiring

> **Visual:** see the Draw.io wiring diagram — [`diagrams/wiring-diagram.drawio`](../diagrams/wiring-diagram.drawio) (open in [draw.io](https://app.diagrams.net) or the VS Code Draw.io Integration extension).

## Power chain (per tracker)

```
Pouch LiPo (+) ──────────────→ TP4056 (B+)
Pouch LiPo (−) ──────────────→ TP4056 (B−)
USB Type-C (VCC) ────────────→ TP4056 (VIN)
USB Type-C (GND) ────────────→ TP4056 (GND)

TP4056 (BAT+) ───────────────→ MT3608 (VIN+)
TP4056 (BAT−) ───────────────→ MT3608 (VIN−)

MT3608 (VOUT+) ──────────────→ ESP8266 5V pin
MT3608 (GND)   ──────────────→ ESP8266 GND

Slide switch: in series with LiPo (+) or MT3608 VOUT+
```

> **Do not** power the ESP8266 directly from the 3.7V cell — it needs 5V. The MT3608 step-up is mandatory.
> **Set the MT3608 trim pot to 5.0V** (measure with a multimeter) before connecting the load.

## I²C — GY-BMI160 → ESP8266

| GY-BMI160 | ESP8266 (NodeMCU / D1-Mini-style) |
|---|---|
| VCC (3.3V) | 3V3 |
| GND | GND |
| SDA | D2 (GPIO4) |
| SCL | D1 (GPIO5) |
| SDO | GND → I²C address **0x68** |
| CSB | GND |

> The Kyware board is NodeMCU-style, so it uses the same **D0–D8** pin labels as a D1 Mini. **Confirm the silkscreen on your exact board** and map to the real GPIOs. If your board labels differ, set the actual GPIO numbers in `defines.h` (see [04-firmware.md](04-firmware.md)).
> A single IMU usually works without external I²C pull-ups. If you add more I²C devices later, add 4.7kΩ pull-ups on SDA and SCL.

## Hot-swap battery (JST-PH 2.0)

- The pouch cell's **JST-PH plug** mates with a **JST-PH socket** soldered to the board.
- The socket's two pins go to **TP4056 B+ / B−** (the battery input).
- Swapping = unplug the dead cell's connector, plug in a charged one. The MT3608 doesn't care which cell is connected — it boosts whatever 3.7V it gets.
- Add a **retaining clip** in the case so the connector doesn't vibrate loose, and **alignment guides** so it can't be inserted reversed.

## Full netlist (per tracker)

| From | To |
|---|---|
| LiPo + (via JST-PH) | TP4056 B+ |
| LiPo − (via JST-PH) | TP4056 B− |
| USB Type-C VCC | TP4056 VIN |
| USB Type-C GND | TP4056 GND |
| TP4056 BAT+ | MT3608 VIN+ |
| TP4056 BAT− | MT3608 VIN− |
| MT3608 VOUT+ | ESP8266 5V |
| MT3608 GND | ESP8266 GND |
| ESP8266 3V3 | GY-BMI160 VCC |
| ESP8266 GND | GY-BMI160 GND |
| ESP8266 D2 (GPIO4) | GY-BMI160 SDA |
| ESP8266 D1 (GPIO5) | GY-BMI160 SCL |
| GY-BMI160 SDO | GND |
| GY-BMI160 CSB | GND |
| Slide switch | in series with LiPo + or MT3608 VOUT+ |

## Battery module (strap-held)

The removable battery lives in a **small 3D-printed module** that sits **under the strap**. The strap holds the module in place — no dock, no magnetic connector. To swap the battery, unclip the module, pop the cell out (JST-PH), and drop in a charged one. Spare cells are charged off-tracker with a standalone TP4056. Full design, workflow, and safety: see [10-battery-module.md](10-battery-module.md).

## Optional

- **Battery voltage divider** → ESP8266 A0 (ADC), for battery % in the SlimeVR server.
- **Schottky diode** (1N5819) between TP4056 BAT+ and MT3608 VIN+ to prevent backflow when powering from USB while the cell is connected.
- **LED:** the ESP8266's onboard LED (D4 / GPIO2 on D1-Mini-style) shows status — no extra part needed.
