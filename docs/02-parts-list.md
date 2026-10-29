# 02 — Parts List (BOM)

Per-tracker bill of materials with purchase links (Tokopedia). Order **5–6 of each** (BMI160s and cheap ESPs have a real DOA rate — keep spares).

## Per-tracker BOM

| # | Part | Spec | Pick | Link | ~Price |
|---|---|---|---|---|---|
| 1 | **MCU** | ESP8266, CH340, micro USB + Type-C | Kyware ESP8266 NodeMCU-style | [Kyware ESP8266 board](https://www.tokopedia.com/kyware/kyware-esp8266-micro-usb-type-c-nodemcu-lua-ch340-v3-wifi-iot-esp-8266-develompent-board-esp-12-1730054147268510742) | — (owned) |
| 2 | **IMU (recommended)** | ICM-45686 + QMC6309 breakout, I²C | **SlimeVR Mumo Breakout Module V1.1** (ICM-45686 + QMC6309) | [SlimeVR Mumo Breakout Module V1.1](https://shop.slimevr.dev/products/slimevr-mumo-breakout-module-v1-icm-45686-qmc6309) | ~$8.00 |
| 2b | IMU (budget) | LSM6DSR + QMC6309 breakout, I²C | LSM6DSR module (AliExpress / Tokopedia) | search: "LSM6DSR module" / "LSM6DSR QMC6309" | ~$3.35 |
| 2c | IMU (fallback, if GY-BMI160 are found) | GY-BMI160, I²C | GY-BMI160 breakout | (previously owned, misplaced) | — |
| 3 | **Battery** | Pouch LiPo 1S 3.7V 1000 mAh, **with PCM** | ZX 523450 (5×34×50 mm) | [ZX 523450 1000mAh with PCM](https://www.tokopedia.com/tokojelek01/zx-523450-1000mah-2c-2a-baterai-lipo-3-7v-dengan-pcm-2a-dan-kabel-55mm-503450-5mm-x-34mm-x-50mm-1730800359683425676) | Rp34.500 |
| 3b | Battery (alt, more runtime) | Pouch LiPo 1S 3.7V 2000 mAh | PALO 103450 (10×34×50 mm) | [PALO 103450 2000mAh](https://www.tokopedia.com/palo-baterai/palo-baterai-103450-3-7v-2000mah-baterai-isi-ulang-lithium-polymer-jst-ph-2-0mm-steker-2-pin-untuk-kamera-gps-navigator-headset-bluetooth-1732702005927511145) | Rp69.000 |
| 4 | **Charger** | TP4056, Type-C, with protection | TP4056 Type-C (Mirorim) | [TP4056 Type-C (Mirorim)](https://www.tokopedia.com/mirorim/tp4056-type-c-18650-battery-charging-module-lithium-ion-protection) | Rp5.000 |
| 5 | **Step-up** | MT3608, 3.7V→5V, 2A | MT3608 module | [MT3608 (Proton Elcom)](https://www.tokopedia.com/proton-elcom/mt3608-kit-dc-dc-2a-step-up-boost-converter-power-module-mini-5-28v-dc) | ~Rp5.000–8.000 |
| 5b | Charger+step-up (alt, simpler) | 2-in-1 TP4056 + boost | Kudaponics 2-in-1 | [2-in-1 TP4056 + step-up](https://www.tokopedia.com/kudaponics/a119-j5019-modul-2-in-1-charger-plus-step-up-adjustable-battery-18650-tp4056-bb-74d-micro-usb-type-c-1731729146084230812) | Rp12.900 |
| 6 | **Battery connector** (hot-swap) | JST-PH 2.0 2-pin socket + plug | JST-PH 2.0 connector pair | search Tokopedia: "konektor JST PH 2.0 2 pin" | ~Rp2.000–5.000 |
| 7 | **Power switch** | Slide switch SPST 6×3×12 mm | slide switch | search Tokopedia: "saklar slide spst" | ~Rp1.000–3.000 |
| 8 | **Wiring** | 22–26 AWG hook-up wire | assorted | search Tokopedia: "kabel jumper" / "kabel hook up" | ~Rp5.000 (roll) |
| 9 | **Strap** | Elastic or leather, ~25 mm wide | elastic band | search Tokopedia: "tali elastis" / "strap" | ~Rp5.000–10.000 |
| 10 | **Misc** | Heat shrink, kapton tape, solder, M2.5 screws | assorted | search Tokopedia: "heat shrink tube", "timah solder" | ~Rp10.000 |

## Cost estimate

| Scenario | Per tracker | 5 trackers |
|---|---|---|
| Base (ICM-45686 Mumo + ZX 1000mAh + TP4056 + MT3608) | ~Rp110.000–120.000 | ~Rp550.000–600.000 |
| Budget (LSM6DSR + ZX 1000mAh + TP4056 + MT3608) | ~Rp75.000–85.000 | ~Rp375.000–425.000 |
| With 2-in-1 charger+boost | +Rp5.000–10.000 | +Rp25.000–50.000 |
| With PALO 2000mAh | +Rp35.000 | +Rp175.000 |

(Excludes the MCU, which is owned. IMU is now a purchase — see the recommendation above.)

Approximate USD conversion: 1 USD ≈ Rp16.000. ICM-45686 Mumo ≈ $8, LSM6DSR ≈ $3.35.

## IMU recommendation

The original GY-BMI160s were misplaced, so the IMU is now a purchase. Per the [SlimeVR IMU comparison](https://docs.slimevr.dev/diy/imu-comparison.html):

| IMU | Tier | Price | Notes |
|---|---|---|---|
| **ICM-45686** | 🟢 Superior | ~$6.70–8.00 | **Best currently available.** Reliable, accurate, stays accurate the longest. Used in the official SlimeVR trackers. |
| **LSM6DSV** | 🟢 Superior | ~$5.80 | About equal to ICM-45686; a bit more temperature-sensitive. |
| **LSM6DSR** | 🟢 Affordable | ~$3.35 | **Recommended budget pick.** Slightly worse sensitivity, lower reset times (25–30 min). |
| BMI160 | 🚫 Avoid | ~$1.50 | Outdated, high drift, ~2/10 DOA. Only as a fallback if the old ones are recovered. |

**Recommendation: ICM-45686** (best performance, and the [SlimeVR Mumo Breakout Module](https://shop.slimevr.dev/products/slimevr-mumo-breakout-module-v1-icm-45686-qmc6309) is purpose-built for SlimeVR with a published schematic + STEP file for the case). **Budget alternative: LSM6DSR.**

> **Mumo V1.1 note:** to use over I²C with an ESP, **jumpers 1–4 must be bridged together** on the module. The module is 1.2 mm thick (not the usual 1.6 mm) with castellated edges.

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
