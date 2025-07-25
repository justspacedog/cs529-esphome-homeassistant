# Dual CS 529 Turntable BLE Integration for ESPHome & Home Assistant

ESPHome-based BLE integration for Dual CS 529 turntables. Connects via BLE to read and control Play/Stop/Tonearm movement, Speed (33/45/78 RPM), Repeat (total & remaining up to 99), Sleep Timer (10 s–42 min), and Bluetooth Pairing Mode. Exposes all controls as Home Assistant switches, numbers and sensors, plus a custom Lovelace Tile UI for status and controls. You'll need to find out the MAC-Adress of your turntable with a bluetooth logger.

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
| `@0PTBTLTxx\r\n`         | Pairing telemetry (LED status)           | `00` = LED off, `01` = LED blue, '02' = LED red                       |

### HomeAssistant Lovelace Tiles
<img width="960" alt="tiles" src="https://github.com/user-attachments/assets/5d92b000-f98f-4cb1-9ac5-59e09fee9ace" />
