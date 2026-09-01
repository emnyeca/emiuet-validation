# VAL-CORE-01

Rev.Bの高影響リスクを一枚で確認する小型統合Validation PCBです。回路図は [`VAL-CORE-01.kicad_sch`](VAL-CORE-01.kicad_sch) です。PCB layoutは今回の範囲外です。

## 回路図に置いたブロック

- USB-C receptacle ×1、Device/UFP CC、VBUS input
- TUSB320（UFP固定、I2C address 0x60想定、INT_N）
- input protection/conditioning候補、5V rail、3.3V regulator候補
- ESP32-S3-MINI-1、EN/reset、BOOT、native USB、flash/recovery
- validation用physical power switch、pilot LED
- 2×3 Kailh Choc matrix（switch/diode/hotswap footprintはPCB時確定）
- slider ×1、button ×1、OLED/I2C header
- SN74AHCT1G125候補、data series resistor、SK6812 MINI-E ×6、各local bypass、bulk capacitor
- TRS MIDI OUT Type-A、isolated TRS MIDI IN Type-A
- TP_5V、TP_3V3、TP_GND、TP_EN、TP_USB_VBUS、TP_CC1、TP_CC2、TP_LED_DATA_3V3、TP_LED_DATA_5V、UART/MIDI TX/RX

## 未確定事項

ESD/TVSとinput fuse/load switch、3.3V regulator、optocoupler、MIDI resistor値、LED series resistor、local bypass、bulk capacitor、connector/footprintは候補段階です。製品回路図・部品datasheet・調達条件と、V0–V2の測定で確定します。

3A advertisementを観測してもhardware/firmware評価上限は1.5A相当です。Default advertisement時のLED budgetはUSB 2.0/3.xをCCから直接区別できない前提で安全側に設定します。
