# CORE-01: MCU・起動・固定USB Device

## 搭載範囲

- ESP32-S3-MINI-1と必要なデカップリング
- ENの外付けRC、BOOT/RESET、書込み・ログ用接続
- GPIO19/20のNative USB D+/D-と固定Device/UFP用USB-C
- CC1/CC2それぞれのDevice用Rd
- D+/D-のESD保護と、実測で必要性を確認する信号フィルタ
- 自己給電Device用の保護済みVBUS検出信号
- 全電源レール、EN、BOOT、D+/D-、VBUS検出点の測定点
- MAT/ANA/UI/MIDI検証基板へ出す診断ヘッダ

## 搭載しないもの

- 充電器、バッテリー、5V/3.3V生成
- 6×13行列、スライダー実装、OLED、TRS出力回路
- TUSB320、Host role検出、DRP/OTG negotiation、Host VBUS制御

## 合格の中心

- 電源投入を繰り返して確実に起動する
- GPIO45/46条件を含む起動安全性を確認する
- Windows等でUSB MIDI + HID Composite Deviceとして列挙・再接続できる
- MIDI/TYPE切替で再列挙せず、stuck note/keyやMCU resetを起こさない
- 物理抜差し後に古いMIDI/HIDイベントを再送せず、再列挙できる
- 連続MIDI演奏とTYPE入力の双方でUSB transportが停止しない
- PWR-01接続時にも起動・列挙結果が変わらない
- 周辺基板未接続でも、全GPIOを安全な状態に保つ

USB-C #2 VBUSは製品正本に従い、給電入力ではなくpresence senseとして
検証する。Host機能はCORE-01の未完項目ではなく`OUT OF SCOPE BY DESIGN`である。
