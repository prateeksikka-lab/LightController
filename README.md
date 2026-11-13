# Light Controller

An Android app that connects to a Wi-Fi light controller and switches four lights on and off. The ESP32/ESP8266 firmware for the controller is in `firmware/`.

## Build the app
1. Open this folder in Android Studio (Ladybug or newer) with **File → Open**.
2. Let Gradle sync. Android Studio downloads Gradle and the SDK pieces it needs.
3. Plug in your phone with USB debugging enabled and press **Run**. To get an installable file, use **Build → Build APK(s)**. The APK is written to `app/build/outputs/apk/debug/app-debug.apk`.

## Flash the controller
1. Open `firmware/LightController/LightController.ino` in the Arduino IDE.
2. Select your ESP32 or ESP8266 board, and set `RELAY_PINS` to match your wiring.
3. Upload the sketch. The board creates a hotspot named **LightController** with the password **12345678**.

## Use it
1. Connect the phone to the **LightController** Wi-Fi. If Android warns that the network has no internet, choose **Stay connected**.
2. Open the app, check that the IP is `192.168.4.1`, and tap **Connect**.
3. Use the four switches, or **All ON** / **All OFF**.

## Protocol
If you already have your own firmware, make it answer these requests:

| Request | Reply |
|---|---|
| `GET /status` | `0101`: one character per light, `1` = ON |
| `GET /switch?id=N&state=on` or `state=off` (N = 1–4) | The new status, e.g. `1101` (any `200 OK` reply also works) |
