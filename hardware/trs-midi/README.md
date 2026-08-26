# MIDI-01: TRS MIDI Type-A

## 搭載範囲

- GPIO43相当の3.3V UART入力
- MIDI仕様に合う5V側の出力回路
- 3.5mm TRS Type-Aコネクタ
- 供給5V、論理入力、各TRS接点の測定点

## 搭載しないもの

- ESP32-S3本体、電源変換、USB/BLE、入力UI

## 合格の中心

- 31250bpsのNote/CC/Pitch Bendを実受信機で受けられる
- Type-Aの接点配置と極性が正しい
- 3.3V GPIOから受信機を直接駆動しない
- UART0コンソールを別経路へ移し、ログがMIDIへ混入しない
- 無接続、短時間の抜差し、連続送信で異常発熱やラッチアップがない
