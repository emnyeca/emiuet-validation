# Emiuet Rev.B Validation

Emiuet Rev.Bで重大な設計ミスだけを、少ない基板数・試行数・費用で先に除去するための検証リポジトリです。製品仕様の正本は [`emnyeca/emiuet`](https://github.com/emnyeca/emiuet) であり、このリポジトリは製品仕様を独自に定義しません。

## 現行の検証対象

専用基板は小型統合基板 **VAL-CORE-01** の1種類だけです。その後、実際のEmiuet Rev.B prototypeで統合確認します。

```text
VAL-CORE-01
  V0 Power / MCU
  V1 Core I/O
  V2 RGB / USB power
        |
        v
Emiuet Rev.B prototype
  V3 integrated acceptance
```

VAL-CORE-01は、ESP32-S3-MINI-1、USB-C Device/UFP、TUSB320、5V/3.3V、物理電源スイッチ、pilot LED、2×3 key matrix、SK6812 MINI-E ×6、slider ×1、button ×1、OLED/I2C、TRS MIDI IN/OUT、測定用テストポイントを一枚に統合します。

回路図の初期たたき台は [`hardware/val-core-01/VAL-CORE-01.kicad_sch`](hardware/val-core-01/VAL-CORE-01.kicad_sch)、構成と未確定事項は [`hardware/val-core-01/README.md`](hardware/val-core-01/README.md) を参照してください。合格条件は [`docs/validation-matrix.md`](docs/validation-matrix.md) が正本です。

## 範囲外

USB Host、DRP、OTG role switching、Host VBUS sourcing、内蔵電池、充電、PowerPath、battery boost、dual USB interactionはRev.Bで採用しないためmandatory validationから除外します。BLEと特定機器相互運用は任意の運用試験です。

旧PWR/CORE/MAT/ANA/UI/MIDI/INT分割案とG0–G9は削除せず [`history/pre-revb`](history/pre-revb/README.md) に保存しています。現行設計へ流用する場合は、Rev.B製品仕様と実測結果を優先してください。
