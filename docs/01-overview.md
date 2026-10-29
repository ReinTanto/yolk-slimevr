# 01 — Overview

## What is SlimeVR?

SlimeVR is open-source software + hardware for **full-body tracking (FBT)** in VR. DIY trackers report their 6DoF pose (position + rotation) over WiFi to a **SlimeVR Server**, which resolves the pose and feeds it to **SteamVR** via an OpenVR driver.

- Firmware: [SlimeVR-Tracker-ESP](https://github.com/SlimeVR/SlimeVR-Tracker-ESP)
- Server: [SlimeVR-Server](https://github.com/SlimeVR/SlimeVR-Server)
- OpenVR driver: [SlimeVR-OpenVR-Driver](https://github.com/SlimeVR/SlimeVR-OpenVR-Driver)
- Docs: https://docs.slimevr.dev

## Tracker count

| Setup | Trackers |
|---|---|
| Full-body tracking (standard) | **5** — chest, left wrist, right wrist, left ankle, right ankle |
| Chest-only | 1 |
| Partial (chest + arms) | 3 |

This build targets **5 trackers**.

## Why these parts

- **IMU: GY-LSM6DS3 (chosen) / ICM-45686 (upgrade)** — the original GY-BMI160s were misplaced, so the IMU is now a purchase. The **GY-LSM6DS3** (LSM6DS3TR-C, supported in firmware as `IMU_LSM6DS3TRC`, cheap on Tokopedia) is chosen; the ICM-45686 is the top-performance upgrade path. The BMI160 is "Avoid" for new builds (outdated, high drift, ~2/10 DOA) — only a fallback if the old ones are recovered. See [02-parts-list.md](02-parts-list.md).
- **ESP8266 (Kyware board)** — cheapest WiFi MCU, the board the whole SlimeVR DIY ecosystem is documented around. **Limitation:** firmware ≥ v0.5.3 supports only **one IMU** per ESP8266 (fine — one IMU per tracker).
- **Pouch LiPo (1S 3.7V)** — 2–3× lighter than an 18650, stable voltage, hot-swappable. Chosen over 18650 for weight on wrists/ankles.
- **3D-printed case** — designed from scratch around the chosen parts; enables a hot-swap battery bay.

## Architecture (per tracker)

```
GY-BMI160 ──(I²C)── ESP8266 ──(WiFi/UDP)── SlimeVR Server ──(OpenVR)── SteamVR
                       │
Pouch LiPo ──→ TP4056 (charge) ──→ MT3608 (3.7V→5V) ──→ ESP8266 5V
```

- The ESP8266 reads the BMI160 over I²C, runs sensor fusion (gyro + accel) in firmware, and streams pose over UDP to the server.
- The server fuses all trackers, applies drift correction, and exposes the pose to SteamVR.

## Build plan summary

1. Procure parts (see [02-parts-list.md](02-parts-list.md))
2. Design + print cases (see [06-case-design.md](06-case-design.md))
3. Wire each tracker (see [03-wiring.md](03-wiring.md), [07-assembly.md](07-assembly.md))
4. Flash firmware (see [04-firmware.md](04-firmware.md))
5. Calibrate IMUs (see [05-calibration.md](05-calibration.md))
6. Set up server + SteamVR (see [08-server-setup.md](08-server-setup.md))
