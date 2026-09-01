# UI-BB-01: UIブレッドボード

> **Historical:** pre-Rev.B分割検証案です。現行mandatory validationではありません。

SSD1315互換OLED、左右/中央ボタン、状態LEDを検証します。Rev.Bの固定USB
Device方針ではTUSB320とのI2C共有を前提にしません。表示更新中にも行列走査、
USB MIDI/HID、BLE、TRS出力のタイミングが崩れないことを確認します。複雑な
メニューは検証対象にしません。
