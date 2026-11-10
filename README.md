# Universal ESP32 Home (starter project)

This repository contains an Android Studio project and starter ESP32 Arduino firmware.

## Current MVP behavior
- Android app opens Android Wi-Fi settings so the user can connect to the ESP32 SoftAP.
- Default ESP32 network: `ESP32_HOME`, password `ChangeMe123`.
- Default ESP32 IP: `192.168.4.1`.
- Eight relay channels with editable labels (long-press a channel name).
- HTTP commands and status reads; the app confirms actual states by reading `/api/status`.
- Device name and IP are saved locally.

## Build Android APK
Open this folder in Android Studio (Giraffe or newer), allow Gradle sync, then:
Build > Build Bundle(s) / APK(s) > Build APK(s).
The APK is normally created at `app/build/outputs/apk/debug/app-debug.apk`.

This environment did not include the Android SDK or Gradle, so no APK binary has been compiled here.

## ESP32 firmware
1. Install ArduinoJson library (v7) in Arduino IDE.
2. Select the correct ESP32 board and upload `esp32_firmware/UniversalESP32_AP.ino`.
3. Change `RELAY_PINS` to GPIOs actually available on your specific ESP32 board.
4. Change the AP password before deployment.
5. Connect the phone to `ESP32_HOME`, then open the app and tap Save device / Check connection.

## Important limitations / safety
- This is a starter MVP, not a production-certified app.
- Android Wi-Fi scanning/selection is controlled by Android. This app opens system Wi-Fi settings; the user selects and connects to the ESP32 AP there.
- This first build uses HTTP status polling/manual refresh, not WebSocket push.
- The current app screen stores one active device profile at a time; the architecture/API is device-agnostic, but the multi-device saved-device manager UI is not yet implemented.
- GPIO pin assignments are example values only. Confirm the exact ESP32-S3 board pinout and relay-driver polarity before connecting hardware.
- Do not connect mains voltage during initial testing. Test with LEDs or a low-voltage load first. Use properly rated isolated relay hardware and enclosure for mains applications.
- Use a unique password and add authentication before exposing control to untrusted networks.
