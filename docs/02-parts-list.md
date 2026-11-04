# 02 — Parts List (BOM)

Per-tracker bill of materials with purchase links (Tokopedia). Order **5–6 of each** (BMI160s and cheap ESPs have a real DOA rate — keep spares).

## Per-tracker BOM

| # | Part | Spec | Pick | Link | ~Price |
|---|---|---|---|---|---|
| 1 | **MCU** | ESP8266, micro USB, 34.2×25.6 mm (compact) | **Wemos D1 Mini** (Supreme) | [Wemos D1 Mini (Supreme)](https://www.tokopedia.com/supreme/wemos-d1-mini-esp8266-arduino-alternatif) | ~Rp15.000–25.000 |
| 2 | **IMU (chosen)** | GY-LSM6DS3 6DoF module (LSM6DS3TR-C + e-compass), I²C | **GY-LSM6DS3** (Supreme, Tokopedia) | [GY-LSM6DS3 6DoF module](https://www.tokopedia.com/supreme/gy-lsm6ds3-6dof-6-axis-always-on-e-compass-accelerometer-gyroscope) | ~Rp30.000–50.000 |
| 2b | IMU (upgrade) | ICM-45686 + QMC6309 breakout, I²C | **SlimeVR Mumo Breakout Module V1.1** | [SlimeVR Mumo Breakout Module V1.1](https://shop.slimevr.dev/products/slimevr-mumo-breakout-module-v1-icm-45686-qmc6309) | ~$8.00 |
| 2c | IMU (fallback, if GY-BMI160 are found) | GY-BMI160, I²C | GY-BMI160 breakout | (previously owned, misplaced) | — |
| 3 | **Battery (chosen)** | Pouch LiPo 1S 3.7V, **small (D1 Mini size)**, wires soldered directly to the shield | Small LiPo (~34×25×5 mm) | search Tokopedia: "baterai lipo kecil 3.7v" / "lipo 3.7v small" | ~Rp20.000–40.000 |
| 3b | Battery (alt, 523450) | Pouch LiPo 1S 3.7V 1000–1500 mAh, 523450 (52×34×5 mm) | 523450 | [523450 1000mAh 52×34mm](https://www.tokopedia.com/a16com/baterai-lithium-polimer-1000mah-523450-52x34mm) | ~Rp30.000–55.000 |
| 3c | Battery (alt, 2000 mAh) | Pouch LiPo 1S 3.7V 2000 mAh, 103450 (10×34×50 mm) | PALO 103450 | [PALO 103450 2000mAh](https://www.tokopedia.com/palo-baterai/palo-baterai-103450-3-7v-2000mah-baterai-isi-ulang-lithium-polymer-jst-ph-2-0mm-steker-2-pin-untuk-kamera-gps-navigator-headset-bluetooth-1732702005927511145) | Rp69.000 |
| 4 | **Battery shield (chosen)** | D1 Mini battery shield, same W×L as D1 Mini, thick (5 mm coil), with battery connector | **Wemos D1 Mini battery shield** | search Tokopedia: "wemos d1 mini battery shield" / "d1 mini shield" | ~Rp15.000–30.000 |
| 4b | Charger (on the shield) | TP4056 + step-up, soldered via pins to the top of the D1 Mini | TP4056 / TP4056+MT3608 module | [TP4056 MT3608 BMS Charger (Supreme ID)](https://www.tokopedia.com/supreme/tp4056-mt3608-li-ion-lipo-bms-charger-dc-dc-boost-converter-micro-usb-power-supply-battery-management-system-1731300325103011443) | Rp9.900 |
| 4c | Charger (alt, separate) | TP4056, Type-C, with protection | TP4056 Type-C (Mirorim) | [TP4056 Type-C (Mirorim)](https://www.tokopedia.com/mirorim/tp4056-type-c-18650-battery-charging-module-lithium-ion-protection) | Rp5.000 |
| 4d | Step-up (alt, separate) | MT3608, 3.7V→5V, 2A | MT3608 module | [MT3608 (Proton Elcom)](https://www.tokopedia.com/proton-elcom/mt3608-kit-dc-dc-2a-step-up-boost-converter-power-module-mini-5-28v-dc) | ~Rp5.000–8.000 |
| 6 | **Battery connector** (on the shield) | JST-PH 2.0 2-pin (comes with the shield) | (included with the shield) | — | — |
| 7 | **Power switch** | **Toggle switch** (SPST), in series with GND | toggle switch | search Tokopedia: "saklar toggle spst" | Rp1.000–3.000 |
| 8 | **Wiring** | 22–26 AWG hook-up wire | assorted | search Tokopedia: "kabel jumper" / "kabel hook up" | ~Rp5.000 (roll) |
| 9 | **Strap** | Elastic or leather, ~25 mm wide | elastic band | search Tokopedia: "tali elastis" / "strap" | ~Rp5.000–10.000 |
| 10 | **Misc** | Heat shrink, kapton tape, solder, M2.5 screws | assorted | search Tokopedia: "heat shrink tube", "timah solder" | ~Rp10.000 |
| 11 | **Battery module** (strap-held, per tracker) | 3D-printed cradle + JST-PH + release tab; sits under the strap | see [10-battery-module.md](10-battery-module.md) | search "konektor JST PH 2.0" + (print cost) | ~Rp2.000–5.000 + print |

## Design change log

| Date | Change | Reason |
|---|---|---|
| 2026-11-03 | **Replaced the TP4056/MT3608 combined board with a D1 Mini battery shield** | The original combined board (Supreme ID) had issues (unreliable) and was slightly larger than the D1 Mini. The battery shield is the same W×L as the D1 Mini, but thicker (a 5 mm tall coil on the board). The shield comes with a battery connector (JST-PH). Attempted to desolder the connector to save space, but it only saves 1 mm because of the 5 mm coil. The charger (TP4056/MT3608) is now soldered via pins to the top of the D1 Mini. The IMU (GY-LSM6DS3) is soldered with copper enamel wire and hot-glued to the backside of the D1 Mini. A **toggle switch** (SPST) is in series with GND. |
| 2026-11-04 | **Changed the battery to a small cell (D1 Mini size), wires soldered directly to the shield** | The 523450 (52×34×5 mm) was too large for the compact build. Replaced with a small LiPo (~34×25×5 mm, the size of the D1 Mini). The battery's wires are soldered **directly** to the battery shield's B+/B− pads (no JST-PH connector). This makes the build more compact — the battery fits alongside the D1 Mini + shield stack. |

## Cost estimate

| Scenario | Per tracker | 5 trackers |
|---|---|---|
| **Chosen (D1 Mini + GY-LSM6DS3 + small LiPo + battery shield + TP4056/MT3608)** | ~Rp100.000–140.000 | ~Rp500.000–700.000 |
| Upgrade (ICM-45686 Mumo + small LiPo + battery shield + TP4056/MT3608) | ~Rp135.000–175.000 | ~Rp675.000–875.000 |
| With 523450 1000mAh (instead of small LiPo) | +Rp10.000–20.000 | +Rp50.000–100.000 |
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
