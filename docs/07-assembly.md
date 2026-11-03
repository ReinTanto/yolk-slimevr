# 07 — Assembly, Testing & Setup

Build **one tracker end-to-end** before starting the next — it surfaces design/wiring problems early. This guide covers assembly, testing, and server setup for the **D1 Mini + GY-LSM6DS3 + 523450 + TP4056/MT3608** build.

## Parts you'll use (per tracker)

| Part | Role |
|---|---|
| Wemos D1 Mini (ESP8266) | WiFi MCU, runs the firmware |
| GY-LSM6DS3 | IMU (gyro + accel + e-compass), I²C — soldered on the backside |
| 523450 1000 mAh LiPo (with PCM) | Battery (hot-swap, JST-PH on the shield) |
| Wemos D1 Mini battery shield | Same W×L as D1 Mini, thick (5 mm coil), with battery connector |
| TP4056 MT3608 BMS board (Supreme ID) | Charger + step-up (3.7V→5V) — soldered via pins to the top of the D1 Mini |
| Toggle switch (SPST) | Power on/off — in series with GND |
| Copper enamel wire | IMU wiring (soldered to the backside of the D1 Mini) |
| Hot glue | Secures the IMU to the backside of the D1 Mini |
| Hook-up wire (22–26 AWG) | Wiring |
| Elastic strap (~25 mm) | Retention (wrist/ankle/chest) |

## Tools

- Soldering iron + solder (thin, 0.5–0.8 mm)
- Multimeter (for voltage + continuity)
- Wire stripper / cutter
- Small screwdriver (for the MT3608 trim pot, if adjustable)
- Computer (for flashing) + USB cables (micro USB data + micro USB for the charger)
- 3D-printed case (empty, verified to fit all parts)

## Phase 1 — Pre-build checks

1. **Verify all parts arrived and work:**
   - **D1 Mini:** plug into USB, confirm the PC sees a COM port (install the CH340/CP210x driver if needed). The onboard LED should light.
   - **GY-LSM6DS3:** check the module's SDO/SA0 pin (sets the I²C address: 0x69 with SDO→VCC, 0x6A with SDO→GND).
   - **TP4056/MT3608 board:** measure the `VOUT+` with a multimeter (no battery, USB power). It should be **5.0V**. If it has a trim pot and reads off, adjust it. If it's fixed and reads 5.0V, you're good.
   - **523450 battery:** measure the voltage — a fresh cell should read **3.7–4.2V**. If it reads below 3.0V, it's deeply discharged (charge it before use).
   - **JST-PH connector:** confirm the plug and socket mate cleanly.
2. **Print the empty case** and verify every part fits (D1 Mini, IMU, battery, power board, switch, USB port). Adjust the CAD if anything is tight.
3. **Read the wiring netlist** ([03-wiring.md](03-wiring.md)) before you start soldering.

## Phase 2 — Assemble the battery shield + charger

Build the power chain first, verify it, then add the IMU.

1. **Mount the D1 Mini on the battery shield** — the shield is the same W×L as the D1 Mini. Align the D1 Mini's pins with the shield's sockets.
2. **Solder the charger (TP4056/MT3608) via pins to the top of the D1 Mini** — the charger's 5V, GND, and VIN pins go to the D1 Mini's top pads.
3. **Solder the toggle switch** in series with GND (between the shield's GND and the D1 Mini's GND).
4. **Verify the power chain:**
   - Plug in USB (micro USB to the battery shield).
   - Measure the shield's 5V output = **5.0V** (under no load).
   - Plug in the JST-PH battery. Measure the battery voltage — it should be **3.7–4.2V**.
   - Measure the 5V output again (under load, with the D1 Mini connected) — it should still be **~5.0V** (a small drop is normal).
   - The D1 Mini's LED should light (it's getting 5V).
   - Toggle the switch OFF → the D1 Mini powers off. Toggle ON → it powers back on.

> **If the D1 Mini's LED doesn't light:** check the 5V/GND solder joints, the toggle switch (is it ON?), and the battery voltage. Use the multimeter to trace the 5V from the shield to the D1 Mini's 5V pin.

## Phase 3 — Solder the IMU (GY-LSM6DS3) on the backside

> **Reference:** see [`media/imu-soldered.jpg`](../media/imu-soldered.jpg) — the GY-LSM6DS3 soldered to the backside of the D1 Mini with copper enamel wire.

5. **Solder the GY-LSM6DS3** to the backside of the D1 Mini using **copper enamel wire**:

| GY-LSM6DS3 | D1 Mini (backside) |
|---|---|
| VCC (3.3V) | 3V3 pad |
| GND | GND pad |
| SDA | D2 (GPIO4) pad |
| SCL | D1 (GPIO5) pad |

6. **Hot-glue the IMU** to the backside of the D1 Mini to secure it.
7. **Confirm the IMU's SDO/SA0 pin** — this sets the I²C address (0x69 or 0x6A). The firmware auto-detects, but it's good to know.
8. **Verify the I²C connection:**
   - Flash a simple I²C scanner sketch (or use the SlimeVR firmware's boot log) to confirm the IMU is detected at 0x69 or 0x6A.
   - If the IMU isn't detected: check SDA/SCL, 3V3, GND, and the SDO/SA0 connection.

> **A single IMU usually works without external I²C pull-ups.** If you add more I²C devices later, add 4.7kΩ pull-ups on SDA and SCL.
> **Copper enamel wire** is ideal for this — the enamel insulation prevents shorts between adjacent wires, and it's thin enough to route in tight spaces.

## Phase 4 — Flash the firmware

9. **Flash the SlimeVR firmware** (see [04-firmware.md](04-firmware.md)) while the D1 Mini is on USB power:
   - Set `#define IMU IMU_LSM6DS3TRC` in `defines.h`.
   - Set `#define PIN_I2C_SDA 4` and `#define PIN_I2C_SCL 5`.
   - Set your WiFi SSID + password.
   - Flash via PlatformIO or the Arduino IDE (board: "Generic ESP8266 Module" or "Wemos D1 Mini").
10. **After flashing, unplug USB** — the D1 Mini runs on battery power.

## Phase 5 — Smoke test (on battery power)

> **Reference:** see [`media/build-demo.mp4`](../media/build-demo.mp4) — the full soldered unit (no case) demonstrated with SlimeVR running on the PC in the background.

11. **Turn on the toggle switch** (battery power).
12. **Verify the tracker boots and connects:**
    - The D1 Mini's LED should blink (WiFi connection).
    - The tracker should appear in the SlimeVR server (see [08-server-setup.md](08-server-setup.md)).
    - The IMU should be detected (check the server's IMU visualizer — pitch/roll should match the tracker's real orientation).
13. **Test the hot-swap:**
    - Unplug the JST-PH battery (tracker should power off).
    - Plug in a charged battery (tracker should power back on).
14. **Test the slide switch:**
    - Switch OFF → tracker powers off.
    - Switch ON → tracker powers on.

> **If the tracker doesn't connect to WiFi:** check the WiFi credentials in the firmware, the 2.4 GHz band (ESP8266 is 2.4 GHz only), and the D1 Mini's power (5V rail). Use the USB serial console to check the boot log.

## Phase 6 — Assemble into the case

15. **Assemble into the case** — battery last, so everything stays accessible:
    - Place the D1 Mini, IMU, and power board in the case.
    - Thread the strap through the strap channel.
    - Insert the battery (JST-PH plug into the socket).
    - Close the case.
16. **Verify the tracker works in the case:**
    - Switch ON → tracker boots, connects to WiFi, appears in the server.
    - The IMU visualizer shows the correct orientation.
    - The strap holds the tracker comfortably.

## Phase 7 — Calibrate the IMU

17. **Calibrate the GY-LSM6DS3** (see [05-calibration.md](05-calibration.md)):
    - Warm the tracker to operating temperature (wear it a few minutes, ~30–40°C).
    - Power up with the IMU lying flat on a stable surface.
    - Leave it still for ~15 seconds on the first side.
    - Place it flat on each of the other 5 sides, waiting for the LED/serial prompt.
    - A long LED flash on the last side = calibration complete.

## Phase 8 — Label and repeat

18. **Label / color-code** the tracker (chest / L-wrist / R-wrist / L-ankle / R-ankle).
19. **Repeat Phases 2–8** for the remaining 4 trackers.

## Quality checks

- **Solder joints:** shiny, concave, no cold/gray joints. Re-flow any suspect joint.
- **I²C:** after wiring, confirm the IMU is detected (serial console / server). If not, check SDA/SCL, 3V3, GND, and the SDO/SA0 connection.
- **5V rail:** measure the TP4056/MT3608 board's `VOUT+` = 5.0 V under load.
- **No shorts:** continuity-check adjacent traces/pads before powering.
- **Strap:** thread and tension the strap; confirm the tracker sits comfortably and the connector is retained.

## Common first-build pitfalls

- **Powering the D1 Mini directly from 3.7V** — won't work. The TP4056/MT3608 board's step-up is mandatory.
- **TP4056/MT3608 board output not set to 5V** — measure and adjust (if it has a trim pot).
- **IMU not detected** — check SDA/SCL, 3V3, GND, and the SDO/SA0 connection.
- **USB port too loose** — charging fails; use a snap-fit or screw-down port.
- **Reverse battery insertion** — add alignment guides to the JST-PH bay.
- **WiFi not connecting** — check the 2.4 GHz band, the WiFi credentials, and the D1 Mini's power.

## Testing checklist (per tracker)

| Test | Pass? |
|---|---|
| D1 Mini LED lights on USB power | ☐ |
| `VOUT+` = 5.0V (no load) | ☐ |
| `VOUT+` = ~5.0V (under load) | ☐ |
| Battery voltage = 3.7–4.2V | ☐ |
| IMU detected at 0x69 or 0x6A | ☐ |
| Firmware flashed successfully | ☐ |
| Tracker boots on battery power | ☐ |
| Tracker connects to WiFi | ☐ |
| Tracker appears in the SlimeVR server | ☐ |
| IMU visualizer shows correct orientation | ☐ |
| Hot-swap works (unplug/plug battery) | ☐ |
| Slide switch works (ON/OFF) | ☐ |
| Tracker works in the case | ☐ |
| IMU calibrated (6-side) | ☐ |

## Server setup

See [08-server-setup.md](08-server-setup.md) for the SlimeVR server + SteamVR OpenVR driver setup.

## Troubleshooting

See [09-troubleshooting.md](09-troubleshooting.md) for common failures and fixes.
