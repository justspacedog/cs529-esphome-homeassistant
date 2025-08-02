# Dual CS 529 Turntable BLE Integration for ESPHome & Home Assistant

ESPHome-based BLE integration for Dual CS 529 turntables. Connects via BLE to control Play/Stop and Speed (33/45/78 RPM) as a fan entity (so you can tell your assistant to spinn "heigher" or "stronger" as Siri doesn't understand "faster" in this context). You can also control the Repeat State (total & remaining up to 99), Sleep Timer (10 s–42 min) and Bluetooth Pairing Mode. You'll need to find out the MAC-Adress of your turntable with a bluetooth logger.

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

### HomeAssistant Lovelace Tiles
<img width="960" alt="tiles" src="https://github.com/user-attachments/assets/5d92b000-f98f-4cb1-9ac5-59e09fee9ace" />
