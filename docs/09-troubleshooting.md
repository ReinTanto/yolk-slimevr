# 09 — Troubleshooting

## Tracker doesn't appear in the server

- **WiFi:** confirm the tracker and server PC are on the same network; check the SSID/password in `defines.h`.
- **Power:** measure the 5V rail (MT3608 output). A brown-out (low battery, unset MT3608) drops the ESP8266 off WiFi.
- **Boot:** hold RST while plugging in USB; check the CH340 driver is installed and the COM port appears.
- **Serial console:** open the server's Serial Console (Settings → Utilities) and read the boot log for errors.

## IMU not detected

- **I²C wiring:** check SDA (GPIO4/D2), SCL (GPIO5/D1), 3V3, GND.
- **Mumo jumpers:** for the ICM-45686 Mumo module, **jumpers 1–4 must be bridged** for I²C.
- **Address:** the IMU address is usually auto-detected; if not, set it explicitly in `defines.h`.
- **DOA sensor:** IMUs (especially cheap ones) have a real DOA rate — swap in a spare and re-test.
- **Pull-ups:** a single IMU usually works without external pull-ups; if adding more I²C devices, add 4.7kΩ on SDA/SCL.

## Flashing fails

- **Data cable:** use a **data** USB cable, not charge-only.
- **CH340 driver:** install it (Windows) so the COM port appears.
- **Boot mode:** hold RST (or GPIO0) while plugging in.
- **Baud/port:** select the correct COM port; try another port/cable.

## Drift / yaw wander

- **Calibrate properly** (6-side, warm tracker) — see [05-calibration.md](05-calibration.md).
- **Let the tracker rest** flat for 20–30 s after power-on.
- **Temperature calibration** (optional) reduces drift.
- **Magnetic environment:** if using a magnetometer (9DoF), keep away from magnets/metal.
- **IMU choice:** the ICM-45686/LSM6DSR have much longer reset times than a BMI160 — if drift is bad, confirm you're not on a BMI160.

## Battery / charging problems

- **Won't charge:** check the USB cable (data cable), the TP4056 charge LED, and the JST-PH connection.
- **Short runtime:** confirm the MT3608 is set to 5V and the cell is a genuine capacity (no-name cells are often mislabeled).
- **Brown-out mid-session:** the cell sagged or the MT3608 droops under load — check the 5V rail under load.
- **Hot-swap fails:** confirm the JST-PH is fully seated and the retaining clip holds; check alignment guides prevent reverse insertion.

## Case / mechanical

- **USB port loose:** use a snap-fit or screw-down port; a poorly fitted port is the #1 charging failure.
- **Connector vibrates loose:** add a retaining clip in the case.
- **Rattle:** tighten the MCU fit (0.2 mm clearance) and secure the battery.
- **Overheating:** add ventilation holes; the ESP8266 + MT3608 get warm.

## DOA parts

- **Order spares** (6 of each consumable) — IMUs and cheap ESPs have a real DOA rate.
- **Swap-and-test** to isolate a dead part before rework.
