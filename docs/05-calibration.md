# 05 — Calibration

Calibration is done **once per IMU** (values are saved to the MCU flash). Re-run it only if you swap IMUs between trackers or after a firmware change that resets calibration.

## ICM-45686 / LSM6DSR / LSM6DSV (SoftFusion IMUs) — 6-side calibration

These are the recommended IMUs for this build. They use the SoftFusion 6-side calibration:

1. **Warm the tracker to operating temperature** first (wear it a few minutes, ~30–40°C) for the best result.
2. Power up with the IMU **lying flat on a stable surface** (or press reset).
3. Leave it still for **~15 seconds** on the first side.
4. Then place it flat on **each of the other 5 sides**, waiting for the LED/serial prompt before moving to the next.
5. A **long LED flash** on the last side = calibration complete. The tracker begins showing rotation in the SlimeVR server.

> Some SoftFusion IMUs (e.g. BNO085, ICM-20948) auto-calibrate and can be used after just resting on a flat surface for 20–30 s. The ICM-45686/LSM6DSR benefit from the explicit 6-side routine above.

## Optional: temperature calibration (reduces drift)

For ICM-45686/LSM6DSR you can optionally run a temperature calibration to cut drift:
1. Cool the tracker below ~15°C (fridge).
2. Power it on and let it warm up gradually — calibration begins automatically when temperature is low.

## GY-BMI160 (fallback only)

If the old GY-BMI160s are recovered and used:
- **Firmware ≥ v0.3.3:** 6-side calibration (same routine as above — flat on each of 6 sides, ~15 s each, long flash on the last).
- **Firmware ≤ v0.3.2:** flip the IMU upside down, reset, flip right-side up, then gently rotate in all 3 axes for ~60 s.
- Calibration data is stored in MCU flash, unique per BMI160.

## General tips

- **Always let a tracker rest flat on a stable surface for 20–30 s** after power-on before use — improves calibration and reduces drift.
- **Calibrate one IMU at a time.**
- If using extensions, calibration data is saved to the main tracker — swapping extensions between main trackers requires recalibration.
- Verify in the server: press **Preview** in a tracker's settings and check that pitch/roll match the real orientation.
