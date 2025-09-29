# Dual CS 529 Turntable — ESPHome BLE Integration (Home Assistant)
<img width="70%" alt="tiles" src="https://github.com/user-attachments/assets/9c797418-38dd-489e-b732-b0d219980ce5"/>


This project lets you control your **Dual CS 529** turntable over **Bluetooth Low Energy (BLE)** with **ESPHome** and **Home Assistant**.  
Instead of fumbling with the clunky official app, you can now say:

> “**Siri, turn on the turntable**”

and the deck responds immediately.

| Before | Now |
|-------|---|
| ![cs529_old_](https://github.com/user-attachments/assets/0123cbd2-4ffd-4cef-b43f-7da8fa1f08fe) | ![cs529_new__](https://github.com/user-attachments/assets/61ee9058-acd1-4a8a-a589-b4524b1b945f) |

## Features

- **Play / Stop** (tonearm control)  
- **Speeds:** 33 / 45 / 78 RPM (mapped as fan “speeds”)  
- **Repeat:** toggle + count (1–99)  
- **Sleep timer:** 10 s → 42 min 30 s  
- **Bluetooth pairing mode** (button press + LED telemetry)  

## Why is it a fan?

We’ve all been there: you put on [a long play that’s actually 45 RPM](https://www.discogs.com/fr/master/3879535-Martin-Luke-Brown-Damn-Look-At-The-View), or albums where [each disc spins at a different speed](https://en.wikipedia.org/wiki/Sable%2C_Fable). With a fan entity you can simply say:  

> “**Siri, set the turntable to 33 RPM**"

and the music sounds right again.

![cs529_new_33rpm](https://github.com/user-attachments/assets/3958c0b9-0dbf-4b6a-8f35-ba7f8204ee85)

## Demo: Repeat & Bluetooth

| Repeat | Bluetooth |
|------|---------|
| ![cs529_new_repeat](https://github.com/user-attachments/assets/c5b1870a-9f09-4203-be2d-d81dd5a2c0ee) | ![cs529_new_bluetooth](https://github.com/user-attachments/assets/b0099530-6d52-40d5-b5fb-fbb1c72c843b) |

> Note: I covered the BLE/Bluetooth LEDs with black foil. BLE stays connected to the ESP32 (blue LED would otherwise be on constantly), while Bluetooth audio is usually disconnected (red LED mostly on). The state of the LED is correctly shown in the Lovelace.

---

### Turntable BLE Command Reference

Below are the raw BLE messages used by the Dual CS 529 turntable, their meanings and valid codes:

| Message                  | Description                              | Codes / Values                                                        |
|--------------------------|------------------------------------------|-----------------------------------------------------------------------|
| `@0PTTTSTxx\r\n`         | Play/Stop/Tonearm state                  | `00` = Stopped<br>`01` = Playing<br>`03` = Starting…<br>`04` = Stopping… |
| `@0PTTTRSxx\r\n`         | Speed in RPM                             | `33`, `45`, `78`                                                      |
| `@0PTTTRPxx\r\n`         | Repeat count (setting)                   | `01`–`99`                                                             |
| `@0PTTTRpxx\r\n`         | Repeat count (remaining)                 | `01`–`99`                                                             |
| `@0PTTTLSxx\r\n`         | Repeat On/Off                            | `01` = On, `00` = Off                                                 |
| `@0PTTTSTSLxxx\r\n`      | Sleep timer (10 s units)                 | `000` = Never, `001` = 10 s … `255` = 42 min 30 s                     |
| `@0PTBTSTxx\r\n`         | Pairing button state                     | `00` = not pressed, `01` = pressed                                    |
| `@0PTBTLTxx\r\n`         | Pairing telemetry (LED status)           | `00` = LED off<br>`01` = LED blue = Connected<br>`02` = LED red = Disconnected<br>`00`+`01` blinking (after press on button) = Connecting...<br>`01`+`02` blinking (after long press on button) = Pairing…                      |
