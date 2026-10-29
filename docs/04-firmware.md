# 04 — Firmware

Flash the [SlimeVR-Tracker-ESP](https://github.com/SlimeVR/SlimeVR-Tracker-ESP) firmware onto each ESP8266.

## 1. Get the firmware

```bash
git clone https://github.com/SlimeVR/SlimeVR-Tracker-ESP.git
cd SlimeVR-Tracker-ESP
```

## 2. Configure `defines.h`

Key settings for this build:

```c
// IMU — pick the one you installed:
#define IMU IMU_LSM6DS3TRC   // chosen (GY-LSM6DS3 module, LSM6DS3TR-C + e-compass)
// #define IMU IMU_ICM45686   // upgrade (SlimeVR Mumo / ICM-45686 + QMC6309)
// #define IMU IMU_LSM6DSR    // alternative (LSM6DSR)
// #define IMU IMU_BMI160     // fallback only, if the old GY-BMI160s are recovered

// I2C pins (D1-Mini / NodeMCU style: D2=GPIO4 SDA, D1=GPIO5 SCL)
#define PIN_I2C_SDA 4
#define PIN_I2C_SCL 5

// I2C address is usually auto-detected; set explicitly only if needed.
// LSM6DS3TR-C: 0x69 (SDO/SA0->VCC) or 0x6A (SDO/SA0->GND) — confirm the module's SDO.
// Mumo V1.1 (ICM-45686, if used): bridge jumpers 1-4 together for I2C use.

// WiFi
#define WIFI_NAME "your-ssid"
#define WIFI_PASS "your-password"

// Tracker port (default 6969)
// #define TRACKER_PORT 6969

// Battery (optional, if you wired a voltage divider to A0)
// #define BAT_EXTERNAL
// #define BAT_SENSE_PIN A0
```

> **Confirm pin labels** on the exact Kyware board and use the real GPIO numbers. NodeMCU-style boards use D0–D8 labels that map to GPIOs (D1=GPIO5, D2=GPIO4). If the silkscreen differs, set the actual GPIO numbers.

## 3. Build & flash (PlatformIO)

```bash
pio run            # build
pio run -t upload  # flash (board selected as d1_mini / nodemcuv2 in platformio.ini)
```

`platformio.ini` board for this build:

```ini
[env:d1_mini]
platform = espressif8266
board = d1_mini        ; or nodemcuv2, matching the Kyware ESP-12 board
```

### Alternative: web flasher

Use a web flasher (e.g. the DIY Firmware Tool in the SlimeVR app Settings tab, or https://slimevr.shinebright.dev) to build + flash in the browser — no local toolchain needed.

## 4. After flashing

1. Power the tracker (or plug in USB).
2. It connects to WiFi and announces itself on the network (UDP port 6969 by default).
3. It appears in the SlimeVR Server (see [08-server-setup.md](08-server-setup.md)).
4. **Calibrate the IMU** before use (see [05-calibration.md](05-calibration.md)).

## Notes

- **ESP8266 = one IMU only** (firmware ≥ v0.5.3). Fine for this build — one IMU per tracker.
- **ICM-45686 / LSM6DSR** use SoftFusion (gyro + accel) in the firmware; the QMC6309 magnetometer on the Mumo module is available for 9DoF but the standard SlimeVR setup runs 6DoF. These are the recommended, well-supported IMUs (unlike the BMI160, which is "experimental"/"Avoid").
- **Calibration data is stored in the MCU flash** and is unique per IMU. If you swap IMUs between trackers, recalibrate.
- **CH340 driver** must be installed for the PC to see the board as a COM port (see [02-parts-list.md](02-parts-list.md)).
