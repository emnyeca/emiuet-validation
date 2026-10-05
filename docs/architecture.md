# Rev.B Validation Architecture

## 役割と正本

製品の回路、GPIO、電力予算、MIDI/HID/RGB挙動は `emnyeca/emiuet` を正本とします。このリポジトリが管理するのは、pre-Rev.Bの記録、VAL-CORE-01の試験、Rev.B prototype acceptance、pass/fail evidenceだけです。

## 二段階構成

### 1. VAL-CORE-01

一枚の統合基板で、製品へ展開する前に次の高影響リスクを切り分けます。

- USB-C一口からの5V給電、保護、3.3V生成
- ESP32-S3-MINI-1のEN/reset/BOOT、初回書込み、再書込み、復旧
- Device/UFPでのUSB MIDI/HID composite enumeration
- Rd＋TLV7022によるDefault／1.5A以上の検出（GPIO37）。1.5Aと3A、orientationは区別しない
- OLEDのI2C通信。USB attach/configured/suspendはUSB stackで確認
- 2×3 matrix、slider ×1、button ×1、pilot LED
- AHCT level shift、SK6812 MINI-E ×6、RMT/DMA、USB MIDI RXからRGBまで
- isolated TRS MIDI INとTRS MIDI OUT
- 物理電源スイッチによる反復power cycle

78キーや78 LEDの配電・温度・電圧降下は小型基板では再現しません。

### 2. Emiuet Rev.B prototype

製品寸法の基板で78 keys、78 RGB LEDs、5V distribution、熱、全I/O同時動作、1～2時間の連続動作を確認します。VAL-CORE-01合格を製品prototypeの合格とみなしません。

## 判定原則

- 文書レビューやビルド成功は実機PASSではない
- 観測値、回路図/BOM/firmware commit、測定条件、波形・ログを結果に残す
- 未実施は `NOT RUN`、設備不足は `BLOCKED`、期待値未達は `FAIL` とする
- ソフトウェア制限で安全側に倒した事項と、hardwareが保証する上限を分けて記録する
- Default current時はUSB世代をCCだけで判定できないため、安全側のLED budgetを評価する

## 境界

USB Host、DRP、Host VBUS、内蔵電池、充電、PowerPath、battery runtime/thermal/reverse-current、dual USBは `OUT OF SCOPE BY DESIGN` です。BLEとCME H12等の個別相互運用は任意で、Rev.B hardware acceptanceを止めません。
