# yolk-slimevr

DIY SlimeVR full-body tracking (FBT) build using **GY-LSM6DS3** IMUs, **ESP8266** microcontrollers, and **pouch LiPo** batteries in **3D-printed** cases, with a **3D-printed charging dock** for the removable cells.

This repo documents the complete plan, parts list (with purchase links), wiring, firmware, calibration, and case design for a 5-tracker SlimeVR setup.

## Contents

| Document | What it covers |
|---|---|
| [docs/01-overview.md](docs/01-overview.md) | What SlimeVR is, tracker count, architecture |
| [docs/02-parts-list.md](docs/02-parts-list.md) | Full BOM with Tokopedia product links |
| [docs/03-wiring.md](docs/03-wiring.md) | Pinout, wiring diagram, power chain |
| [docs/04-firmware.md](docs/04-firmware.md) | Flashing SlimeVR firmware, `defines.h` config |
| [docs/05-calibration.md](docs/05-calibration.md) | BMI160 6-side calibration + temperature calibration |
| [docs/06-case-design.md](docs/06-case-design.md) | 3D case design, dimensions, hot-swap battery |
| [docs/07-assembly.md](docs/07-assembly.md) | Step-by-step build guide |
| [docs/08-server-setup.md](docs/08-server-setup.md) | SlimeVR server + SteamVR OpenVR driver |
| [docs/09-troubleshooting.md](docs/09-troubleshooting.md) | Common failures and fixes |
| [docs/10-charging-dock.md](docs/10-charging-dock.md) | Charging dock for the removable cells |

## Quick parts summary

| Part | Pick |
|---|---|
| MCU | Kyware ESP8266 (NodeMCU-style, CH340, micro USB + Type-C) |
| IMU | **GY-LSM6DS3** (LSM6DS3TR-C 6DoF + e-compass, I²C — Tokopedia) — *upgrade: ICM-45686 Mumo* |
| Battery | Pouch LiPo 1S 3.7V **1000 mAh** (523450, 52×34 mm, hot-swappable, JST-PH) |
| Charger | TP4056 module (Type-C, with protection) |
| Step-up | MT3608 module (3.7V → 5V) |
| Case | 3D-printed (designed around the parts) |
| Charging dock | 3D-printed 5-slot TP4056 bank (recharges the removable cells) — *optional: magnetic pogo pins* |

> The original GY-BMI160s were misplaced, so the IMU is now a purchase. The **GY-LSM6DS3** (LSM6DS3TR-C, supported in firmware as `IMU_LSM6DS3TRC`, cheap on Tokopedia) is chosen; the ICM-45686 is the upgrade path. See [docs/02-parts-list.md](docs/02-parts-list.md).

## Tracker count

- **5 trackers** for full-body tracking (chest, 2 wrists, 2 ankles)
- **1 tracker** for chest-only

## Status

Planning / parts procurement. See [docs/02-parts-list.md](docs/02-parts-list.md) for purchase links.
