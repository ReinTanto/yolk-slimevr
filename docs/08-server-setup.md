# 08 — Server + SteamVR Setup

The SlimeVR Server receives tracker poses over WiFi and feeds them to SteamVR via the OpenVR driver.

## 1. Install the SlimeVR Server

- **Windows:** download the installer from the [SlimeVR-Server releases](https://github.com/SlimeVR/SlimeVR-Server/releases) — it bundles the OpenVR driver.
- **Linux / macOS:** download `slimevr.jar` from the [releases](https://github.com/SlimeVR/SlimeVR-Server/releases/latest/download/slimevr.jar) and run with Java:
  ```bash
  java -jar slimevr.jar
  ```

The server exposes a web UI (default `http://localhost:30003`). Trackers appear there once they connect to the same WiFi.

## 2. (Windows) OpenVR driver

The Windows installer handles this automatically. For **Linux**, install manually:
1. Download the [slimevr-openvr-driver](https://github.com/SlimeVR/SlimeVR-OpenVR-Driver/releases/latest/download/slimevr-openvr-driver-x64-linux.zip).
2. Extract, then register with SteamVR:
   ```bash
   ~/.steam/steam/steamapps/common/SteamVR/bin/vrpathreg.sh adddriver /path/to/slimevr
   ```
3. Restart SteamVR.
4. Set the SteamVR launch argument (Steam → SteamVR → Properties → Launch options):
   ```
   PRESSURE_VESSEL_FILESYSTEMS_RW="$XDG_RUNTIME_DIR/SlimeVRDriver" %command%
   ```

## 3. Connect the trackers

1. Ensure trackers and the server PC are on the **same WiFi network**.
2. Power on each tracker — it announces itself (UDP, default port 6969).
3. They appear in the server UI. **Calibrate each** (see [05-calibration.md](05-calibration.md)).
4. In the server, assign each tracker to a body part (chest, L/R wrist, L/R ankle).

## 4. Verify in SteamVR

1. Launch SteamVR.
2. The SlimeVR driver shows the tracked body parts.
3. Move around — confirm the virtual body follows you.
4. Adjust sensitivity/offset in the server UI as needed.

## Minimum tracker count

- **5 trackers** for full-body (chest, 2 wrists, 2 ankles).
- **1 tracker** for chest-only.

## Tips

- Keep the server PC and trackers on a **stable 2.4 GHz or 5 GHz** network; avoid congested networks.
- If a tracker drops, check its battery (brown-out) and WiFi signal.
- Use the server's **Serial Console** (Settings → Utilities) to debug individual trackers.
