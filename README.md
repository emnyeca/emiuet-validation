# Emiuet Validation

Rev.Bへ進む前に、Emiuetの機能を小さな単位で実測し、不具合の場所を
特定できる状態にするための検証プロジェクトです。

Emiuetは、内蔵バッテリー、充電、PowerPath、必要な電源レールを本体に
持つ、単体完結のMIDIキーボードです。HearthやEUB-BUSは製品の通常動作に
必要ありません。

USB-C #1 is the charging/power input. USB-C #2 is a fixed USB 2.0
Device/UFP port that exposes USB MIDI + USB HID Keyboard as one composite
device. USB Host, DRP, OTG role switching, and Host VBUS sourcing are outside
the Rev.B product and validation scope by design.

## このリポジトリの役割

- 機能ごとの回路図、PCB、ブレッドボード構成を分離する
- 測定点、試験条件、合否基準を製造前に決める
- 実測結果と不具合の再現条件を残す
- 合格した回路だけをcontroller-integration基板へ集約する
- integration基板の合格後に、Emiuet Rev.Bへ移植する

Rev.Aの回路をそのまま正解とは扱いません。流用箇所には出典を記録し、
各検証基板で確認できた事実と推測を分けます。

## 検証単位

| ID | 対象 | 形態 | 主に切り分けるもの |
|---|---|---|---|
| PWR-01 | Emiuet内蔵電源 | PCB | 充電、PowerPath、5V/3.3V、逆流、状態信号 |
| CORE-01 | MCU・起動・固定USB Device | PCB | ESP32-S3、EN/BOOT、UFP・Composite列挙・再接続 |
| MAT-BB-01 | 2×4キー行列 | ブレッドボード | ダイオード方向、走査、デバウンス |
| MAT-01 | 6×13キー行列 | PCB | 全78キー、ゴースト、配線・コネクタ |
| ANA-01 | 3スライダー | PCB | ADC、平滑化、戻り値、電源・走査ノイズ |
| UI-BB-01 | OLED・3ボタン・LED | ブレッドボード | I2C共有、入力、表示更新の影響 |
| MIDI-01 | TRS MIDI Type-A | PCB | 5V電流ループ、極性、31250bps、受信互換性 |
| INT-01 | コントローラ統合 | PCB | 合格済み機能間の干渉、起動、同時負荷 |

詳細な順序と合格条件は [docs/validation-matrix.md](docs/validation-matrix.md)、
回路の境界は [docs/architecture.md](docs/architecture.md) を正とします。

## ディレクトリ

```text
docs/                   方針、試験マトリクス、測定結果
hardware/               機能別KiCadプロジェクト
breadboards/            PCB化前の最小検証
firmware/diagnostics/   検証専用ファームウェアとログ仕様
```

## 現在地

検証境界と合格ゲートを定義済みです。次の実装はPWR-01とCORE-01の
回路図作成です。PWR-01の定格値を確定する前に、Rev.Bの最大負荷と充電
時間から電流予算を決める必要があります。
