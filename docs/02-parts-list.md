# 02 — Parts List (BOM)

Per-tracker bill of materials with purchase links (Tokopedia). Order **5–6 of each** (BMI160s and cheap ESPs have a real DOA rate — keep spares).

## Per-tracker BOM

| # | Part | Spec | Pick | Link | ~Price |
|---|---|---|---|---|---|
| 1 | **MCU** | ESP8266, CH340, micro USB + Type-C | Kyware ESP8266 NodeMCU-style | [Kyware ESP8266 board](https://www.tokopedia.com/kyware/kyware-esp8266-micro-usb-type-c-nodemcu-lua-ch340-v3-wifi-iot-esp-8266-develompent-board-esp-12-1730054147268510742) | — (owned) |
| 2 | **IMU (chosen)** | GY-LSM6DS3 6DoF module (LSM6DS3TR-C + e-compass), I²C | **GY-LSM6DS3** (Supreme, Tokopedia) | [GY-LSM6DS3 6DoF module](https://www.tokopedia.com/supreme/gy-lsm6ds3-6dof-6-axis-always-on-e-compass-accelerometer-gyroscope) | ~Rp30.000–50.000 |
| 2b | IMU (upgrade) | ICM-45686 + QMC6309 breakout, I²C | **SlimeVR Mumo Breakout Module V1.1** | [SlimeVR Mumo Breakout Module V1.1](https://shop.slimevr.dev/products/slimevr-mumo-breakout-module-v1-icm-45686-qmc6309) | ~$8.00 |
| 2c | IMU (fallback, if GY-BMI160 are found) | GY-BMI160, I²C | GY-BMI160 breakout | (previously owned, misplaced) | — |
| 3 | **Battery (chosen)** | Pouch LiPo 1S 3.7V **1000 mAh**, 523450 (52×34×5 mm) | 523450 1000 mAh (a16com, Tokopedia) | [523450 1000mAh 52×34mm](https://www.tokopedia.com/a16com/baterai-lithium-polimer-1000mah-523450-52x34mm) | ~Rp30.000–40.000 |
| 3b | Battery (alt, 1500 mAh) | Pouch LiPo 1S 3.7V 1500 mAh, 523450 (52×34×5 mm) | 523450 1500 mAh | (higher-capacity 523450 variant) | ~Rp40.000–55.000 |
| 3c | Battery (alt, 2000 mAh) | Pouch LiPo 1S 3.7V 2000 mAh, 103450 (10×34×50 mm) | PALO 103450 | [PALO 103450 2000mAh](https://www.tokopedia.com/palo-baterai/palo-baterai-103450-3-7v-2000mah-baterai-isi-ulang-lithium-polymer-jst-ph-2-0mm-steker-2-pin-untuk-kamera-gps-navigator-headset-bluetooth-1732702005927511145) | Rp69.000 |
| 4 | **Charger + step-up (chosen)** | TP4056 + MT3608 combined, micro USB, with protection | **TP4056 MT3608 BMS Charger** (Supreme ID) | [TP4056 MT3608 BMS Charger (Supreme ID)](https://www.tokopedia.com/supreme/tp4056-mt3608-li-ion-lipo-bms-charger-dc-dc-boost-converter-micro-usb-power-supply-battery-management-system-1731300325103011443) | Rp9.900 |
| 4b | Charger (alt, separate) | TP4056, Type-C, with protection | TP4056 Type-C (Mirorim) | [TP4056 Type-C (Mirorim)](https://www.tokopedia.com/mirorim/tp4056-type-c-18650-battery-charging-module-lithium-ion-protection) | Rp5.000 |
| 4c | Step-up (alt, separate) | MT3608, 3.7V→5V, 2A | MT3608 module | [MT3608 (Proton Elcom)](https://www.tokopedia.com/proton-elcom/mt3608-kit-dc-dc-2a-step-up-boost-converter-power-module-mini-5-28v-dc) | ~Rp5.000–8.000 |
| 4d | Charger+step-up (alt) | 2-in-1 TP4056 + boost, Type-C | Kudaponics 2-in-1 | [2-in-1 TP4056 + step-up](https://www.tokopedia.com/kudaponics/a119-j5019-modul-2-in-1-charger-plus-step-up-adjustable-battery-18650-tp4056-bb-74d-micro-usb-type-c-1731729146084230812) | Rp12.900 |
| 6 | **Battery connector** (hot-swap) | JST-PH 2.0 2-pin socket + plug | JST-PH 2.0 connector pair | search Tokopedia: "konektor JST PH 2.0 2 pin" | ~Rp2.000–5.000 |
| 7 | **Power switch** | Slide switch SPST 6×3×12 mm | slide switch | search Tokopedia: "saklar slide spst" | ~Rp1.000–3.000 |
| 8 | **Wiring** | 22–26 AWG hook-up wire | assorted | search Tokopedia: "kabel jumper" / "kabel hook up" | ~Rp5.000 (roll) |
| 9 | **Strap** | Elastic or leather, ~25 mm wide | elastic band | search Tokopedia: "tali elastis" / "strap" | ~Rp5.000–10.000 |
| 10 | **Misc** | Heat shrink, kapton tape, solder, M2.5 screws | assorted | search Tokopedia: "heat shrink tube", "timah solder" | ~Rp10.000 |
| 11 | **Battery module** (strap-held, per tracker) | 3D-printed cradle + JST-PH + release tab; sits under the strap | see [10-battery-module.md](10-battery-module.md) | search "konektor JST PH 2.0" + (print cost) | ~Rp2.000–5.000 + print |

## Cost estimate

| Scenario | Per tracker | 5 trackers |
|---|---|---|
| **Chosen (GY-LSM6DS3 + 523450 1000mAh + TP4056/MT3608 combined)** | ~Rp75.000–95.000 | ~Rp375.000–475.000 |
| Upgrade (ICM-45686 Mumo + 523450 1000mAh + TP4056/MT3608 combined) | ~Rp115.000–135.000 | ~Rp575.000–675.000 |
| With separate TP4056 + MT3608 (instead of combined) | −Rp3.000–5.000 | −Rp15.000–25.000 |
| With 523450 1500mAh | +Rp10.000–20.000 | +Rp50.000–100.000 |
| With PALO 2000mAh (103450) | +Rp30.000–40.000 | +Rp150.000–200.000 |

(Excludes the MCU, which is owned. IMU + battery are purchases — see the recommendations above.)

Approximate USD conversion: 1 USD ≈ Rp16.000. GY-LSM6DS3 ≈ $2–3, 523450 1000mAh ≈ $2–3, ICM-45686 Mumo ≈ $8.

## IMU recommendation

The original GY-BMI160s were misplaced, so the IMU is now a purchase. Per the [SlimeVR IMU comparison](https://docs.slimevr.dev/diy/imu-comparison.html) and the [firmware compatibility list](https://github.com/SlimeVR/SlimeVR-Tracker-ESP):

| IMU | Tier | Price | Notes |
|---|---|---|---|
| **GY-LSM6DS3** ✅ chosen | 🟢 (SoftFusion) | ~Rp30.000–50.000 | **Chosen — GY-LSM6DS3 module (LSM6DS3TR-C + e-compass) on Tokopedia.** Supported in firmware as `IMU_LSM6DS3TRC` (SoftFusion, gyro + accel). |
| ICM-45686 | 🟢 Superior | ~$6.70–8.00 | Best currently available (upgrade path). Used in the official SlimeVR trackers. |
| LSM6DSV | 🟢 Superior | ~$5.80 | About equal to ICM-45686; a bit more temperature-sensitive. |
| LSM6DSR | 🟢 Affordable | ~$3.35 | Recommended budget pick (alternative). |
| BMI160 | 🚫 Avoid | ~$1.50 | Outdated, high drift, ~2/10 DOA. Only a fallback if the old ones are recovered. |

**Chosen: GY-LSM6DS3** — a well-supported SoftFusion IMU (the firmware lists `IMU_LSM6DS3TRC` alongside LSM6DSV/LSM6DSO/LSM6DSR/ICM-42688/BMI270). The module also carries an e-compass (magnetometer), but the standard SlimeVR setup runs **6DoF (gyro + accel)**, so the magnetometer is optional. If you later want the top performance, the upgrade path is the **ICM-45686** ([SlimeVR Mumo Breakout Module](https://shop.slimevr.dev/products/slimevr-mumo-breakout-module-v1-icm-45686-qmc6309), which ships with a published schematic + STEP file for the case).

> **GY-LSM6DS3 note:** the LSM6DS3TR-C I²C address is **0x69** (SDO/SA0→VCC) or **0x6A** (SDO/SA0→GND) — the firmware auto-detects, but confirm the module's SDO pin. Use `#define IMU IMU_LSM6DS3TRC` in `defines.h`.

## Buying notes

- **Order 6 of each consumable** (batteries, chargers, switches, IMUs) — IMUs and cheap ESPs have a real DOA rate.
- **Get the pouch cell WITH PCM** (protection circuit module). A bare pouch cell with no protection can be ruined by over-discharge or is a fire hazard if punctured. The ZX "dengan PCM" variant includes it.
- **JST-PH 2.0** is the standard LiPo connector and what most pouch cells ship with — use it for the hot-swap.
- **USB cable:** get a **data** cable (not charge-only) for flashing, and a Type-C cable for charging (matches the Kyware board + TP4056 Type-C).

## CH340 driver

The Kyware board uses a **CH340** USB-serial chip. Install the driver so the PC sees it as a COM port when flashing:
- **Windows:** installer from [WCH](https://www.wch-ic.com/downloads/CH341SER_EXE.html) or the Wemos wiki (https://www.wemos.cc/en/latest/ch340_driver.html)
- **Linux / macOS 10.15+:** usually built-in (`ls /dev/ttyUSB*`)
- If the board isn't detected: use a **data** cable, try another port, or hold **RST** while plugging in.
