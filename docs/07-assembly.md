# 07 — Assembly (step-by-step)

Build one tracker end-to-end before starting the next — it surfaces design/wiring problems early.

## Per-tracker build order

1. **Print the empty case** and verify every part fits (MCU, IMU, battery, TP4056, MT3608, switch, USB port). Adjust the CAD if anything is tight.
2. **Solder the JST-PH 2.0 socket** to the board (battery input → TP4056 B+/B−).
3. **Solder the TP4056** (B+/B− to the JST socket; VIN/GND to the USB Type-C).
4. **Solder the MT3608** (VIN+/VIN− from TP4056 BAT+/BAT−; VOUT+/GND to the ESP8266 5V/GND).
5. **Set the MT3608 trim pot to 5.0 V** (measure with a multimeter before connecting the load).
6. **Wire the IMU** (Mumo / GY-BMI160) to the ESP8266 I²C pins (SDA=GPIO4/D2, SCL=GPIO5/D1) + 3V3 + GND. For the Mumo, **bridge jumpers 1–4** for I²C.
7. **Wire the slide switch** in series with the battery line (or MT3608 VOUT+).
8. **Solder the USB Type-C** to the case/TP4056.
9. **Flash the firmware** (see [04-firmware.md](04-firmware.md)) while the board is on USB power.
10. **Smoke test on USB power:** board boots, connects to WiFi, appears in the SlimeVR server, IMU is detected.
11. **Assemble into the case** — battery last, so everything stays accessible.
12. **Test on battery power** (switch on). Confirm the tracker stays connected and the IMU reports.
13. **Calibrate the IMU** (see [05-calibration.md](05-calibration.md)).
14. **Label / color-code** the tracker (chest / L-wrist / R-wrist / L-ankle / R-ankle).

## Wiring reference

See [03-wiring.md](03-wiring.md) for the full netlist and power chain.

## Quality checks

- **Solder joints:** shiny, concave, no cold/gray joints. Re-flow any suspect joint.
- **I²C:** after wiring, confirm the IMU is detected (serial console / server). If not, check SDA/SCL, 3V3, GND, and (for Mumo) the jumper bridge.
- **5V rail:** measure MT3608 output = 5.0 V under load.
- **No shorts:** continuity-check adjacent traces/pads before powering.
- **Strap:** thread and tension the strap; confirm the tracker sits comfortably and the connector is retained.

## Common first-build pitfalls

- **Forgetting the MT3608** — powering the ESP8266 directly from 3.7V won't work.
- **MT3608 not set to 5V** — the trim pot defaults low; measure and adjust.
- **Mumo jumpers not bridged** — I²C won't work unless jumpers 1–4 are connected.
- **USB port too loose** — charging fails; use a snap-fit or screw-down port.
- **Reverse battery insertion** — add alignment guides to the JST-PH bay.
