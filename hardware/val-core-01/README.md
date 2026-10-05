# VAL-CORE-01

Rev.Bの高影響リスクを一枚で確認する小型統合Validation PCBです。回路図は [`VAL-CORE-01.kicad_sch`](VAL-CORE-01.kicad_sch) です。PCB layoutは今回の範囲外です。

## 検証対象と実装状況

以下は完成時の検証対象です。回路図は未完成で、一覧の全回路が実装済みという意味ではありません。2026-10-05に旧TUSB320を撤去し、製品案と同じRd＋TLV7022、RC filter、VREF、pull-upを実接続しました。電源・MIDIはplaceholderで、matrix、slider、button、OLED、reset/BOOT、power switch、test point、pixel bypassはまだ部品・接続が揃っていません。製造不可。

- USB-C receptacle ×1、Device/UFP CC、VBUS input
- Rd 5.1k ×2＋TLV7022、GPIO37へ `USB_CC_1A5_N`（Low = 1.5A以上）
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

1.5Aと3Aのsourceは別々に試験しますが、回路の出力は共通の「1.5A以上」です。orientationも検出しません。Default時のUSB制限はconfiguration/suspendを含めて総入力電流で確認し、LED budgetだけで適合を判断しません。

機械確認は隣接製品repoから `python tools/verify_hardware.py --schematic ../emiuet-validation/hardware/val-core-01/VAL-CORE-01.kicad_sch`（KiCad 10.0.3）。ERC、netlist、BOM、SVGを製品repoのgit対象外 `build/hardware/` へ出力します。実測と製造承認は別です。
