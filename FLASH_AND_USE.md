# yolk-slimevr — Flash, Diagnose, Use

Agent-readable guide for the per-tracker workflow: flashing firmware, diagnosing
the failure modes found during the first build, and using the tracker after.
Hardware: **Wemos D1 Mini (ESP8266) + GY-LSM6DS3 (LSM6DS3TR-C) + TP4056/MT3608 board + pouch LiPo**.
Wiring: VCC→3V3, GND, SDA→D2 (GPIO4), SCL→D1 (GPIO5), SDO/SA0→GND (I²C addr **0x6A**).

No WiFi credentials are stored in this repo. The tracker gets its WiFi password
once via the SlimeVR app (SmartConfig) and keeps it in flash forever.

---

## 1. Flash the firmware

### Prerequisites (one-time, per PC)

- `pip install platformio` (invoke as `python -m platformio`)
- **CH340 driver** installed (D1 must show as a COM port)
- Firmware clone: `git clone https://github.com/SlimeVR/SlimeVR-Tracker-ESP.git`

### The one setting that matters

Edit `board-defaults.json` → `defaults.BOARD_WEMOSD1MINI.values.SENSORS[0]`:

```json
{ "protocol": "I2C", "imu": "IMU_LSM6DS3TRC", "address": 106,
  "int": "D5", "rotation": "DEG_270", "scl": "D1", "sda": "D2" }
```

The preprocessor injects `SENSOR_DESC_LIST` from this file — it overrides
`defines.h`. The default `IMU_AUTO` is **broken for this IMU** (see gotcha below).

### Flash

```bash
python -m platformio run -e BOARD_WEMOSD1MINI -t upload --upload-port COMx
```

First build downloads the ESP8266 toolchain (~5 min); later builds ~30 s.

### Verify (mandatory)

Read the boot log over serial @ 115200 (SlimeVR server UI → Settings →
Utilities → Serial Console, or any serial monitor). A **healthy** boot contains:

```
[INFO ] [SensorManager] Sensor 0 configured
[INFO ] [SensorManager] 1 sensor(s) configured
[INFO ] [WiFiHandler] Connected successfully to SSID '<your-ssid>', IP address <ip>
[DEBUG] [UDPConnection] Handshake successful, server is <pc-ip>:6969
```

If the log shows `0 sensor(s) configured`, the flash is broken — see §2.

---

## 2. Diagnosis (failure modes found in this build)

**First step for any problem: read the boot log over serial.** It tells you
which layer is broken (sensor / WiFi / server / none).

### LED patterns (D1 onboard LED, D4/GPIO2, active-low)

| LED | Meaning |
|---|---|
| steady off | all good |
| 3 blinks, ~3 s pause | WiFi connecting |
| short flicker every ~1 s | WiFi OK, server unreachable |
| 5 blinks, every ~1 s | IMU error |
| rapid single pulse (~3×/s) | low battery (can be a false alarm — see below) |

### Failure modes

1. **`0 sensor(s) configured` + `Can't find sensor type` + 5-blink LED, but WiFi/server OK**
   → The firmware's auto-detect list (`src/sensors/SensorBuilder.h`,
   `findSensorType`) has `SoftFusionLSM6DS3TRC` **commented out** in the
   current `main` branch, so `IMU_AUTO` can never find this module. The
   "I2C device found at 0x6a" line that follows is only a *diagnostic* scan —
   it never re-configures the sensor.
   **Fix:** flash with explicit `"imu": "IMU_LSM6DS3TRC"` in
   `board-defaults.json` (compile-time template path, fully enabled).
   **Never use the app's web flasher for this build** — it builds `main` with
   `IMU_AUTO` defaults and produces this broken firmware.

2. **`Mandatory sensor 1 not found at address I2C(0x5a)`**
   → Wrong I²C address: JSON numbers are **decimal**. 0x6A = **106**, not 90
   (90 = 0x5A). Set `"address": 106`.

3. **Tracker on WiFi + handshake OK, but server UI shows no trackers**
   → Check in this order:
   a. Windows Firewall: run `server\firewall.bat` (needs UAC; adds UDP 6969,
      TCP 21110, UDP 8266 rules).
   b. Network profile: the server warns if adapters are **Public** — set to
      Private (elevated): `Set-NetConnectionProfile -Name "<name>" -NetworkCategory Private`.
   c. Same subnet: tracker and PC must share a LAN segment (check the router's
      DHCP client list; watch for 2.4/5 GHz on different VLANs or AP isolation).
   d. If the boot log itself shows `0 sensor(s) configured`, it's failure mode 1,
      not a network problem.

4. **SlimeVR GUI (SlimeVR.exe) says "incompatible/different java version"**
   → On Windows the GUI finds Java only via bundled JRE (absent in the zip) or
      `JAVA_HOME` (it does **not** check PATH). Set it:
      `setx JAVA_HOME "C:\Program Files\Eclipse Adoptium\jdk-<ver>-hotspot"`
      (any JDK ≥ 17 works; the GUI-launched server then works).
      Headless alternative: `java -jar slimevr.jar run`.

5. **`could not open port 'COMx': Access is denied` during upload**
   → Another process holds the port — almost always the SlimeVR **Serial
      Console** left open. Close it, retry.

6. **Rapid-pulse LED (low battery) with no battery divider wired**
   → False alarm: `BATTERY_MONITOR=BAT_EXTERNAL` reads a floating A0. Harmless
      for tracking; wire the voltage divider (100k/220k per board defaults) or
      ignore.

### Serial log quick reference

- `Reset reason: External System` = normal (USB reset / power cycle)
- `Sketch MD5` changes = firmware was re-flashed (compare to catch accidental
  web-flasher overwrites)
- `FIRMWARE_VERSION: "main"` = built from main branch (web flasher) — suspect
  it if sensors don't start
- `Handshake successful, server is <ip>:6969` = tracker ↔ server link works

---

## 3. Using the tracker after flashing

1. **WiFi (one-time, per tracker):** SlimeVR mobile app → Settings → WiFi
   setup (SmartConfig). Phone must be on the home WiFi. The app pushes the
   SSID + password to the tracker; it's stored in flash and reused on every
   power-on. (Alternative: hardcode via `-DWIFI_CREDS_SSID` /
   `-DWIFI_CREDS_PASSWD` build flags in `platformio.ini` — keep real
   passwords out of the repo.)
2. **Server:** extract `SlimeVR-win64.zip`, set `JAVA_HOME` (failure mode 4),
   run `firewall.bat` (failure mode 3a), launch `SlimeVR.exe`. UI at
   `http://localhost:30003`.
3. **Tracker appears** in the server UI (announces on UDP 6969).
4. **Calibrate** — 6-side routine (docs/05-calibration.md): rest the tracker on
   each of its 6 faces for a few seconds, prompted by the app/server. Stored in
   tracker flash; redo only if you swap IMUs.
5. **Assign** the tracker to a body part (chest / wrist / ankle) in the server UI.
6. **SteamVR:** launch; the SlimeVR OpenVR driver shows the tracked part.
   1 tracker = chest-only (valid test); 5 trackers = full body.

### Day-to-day

- Power: LiPo via the TP4056/MT3608 board (or USB for testing). Cell swap =
  unplug JST-PH, plug charged cell.
- LED steady off = healthy; consult the LED table in §2 when in doubt.
- Debugging: server UI → Settings → Utilities → **Serial Console** shows the
  live tracker log (close it before re-flashing — failure mode 5).
