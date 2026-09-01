# INT-01: コントローラ統合

> **Historical:** pre-Rev.B分割検証案です。現行mandatory validationではありません。

Rev.Bの外形・78キースイッチを含む完成基板へ進む前の、中間統合PCBです。

## 統合するもの

- PWR-01で合格したEmiuet内蔵電源
- CORE-01で合格したESP32-S3、起動、固定USB Device/UFP
- MAT-01相当の行列インターフェース
- ANA-01、UI-BB-01、MIDI-01で合格した回路
- BLE-MIDIの実transport

行列は小型テストパネルまたはMAT-01をヘッダ接続し、最終筐体や装飾基板の
問題を混ぜません。機能ブロックごとに電源切り離しジャンパと測定点を残します。

## 合格の中心

- Hearthなしで、電池のみ・充電中・USB-C #2接続中に動作する
- 電源遷移で意図しないリセットやNote Off欠落が起きない
- 行列演奏からUSB MIDIを連続送信でき、USB + TRSおよびUSB + BLEの同時動作でも応答が保たれる
- TYPE Modeで文字、数字、Space、Enter、Backspace、modifier、矢印、Fn mappingを入力できる
- MIDI/TYPE切替を反復しても再列挙、stuck note/key、MCU resetが起きない
- バッテリー動作中のUSB-C #2抜差し後にComposite Deviceとして復帰し、古いイベントを再送しない
- OLED更新中にもUSB MIDI/HID、行列、ADC、BLE、TRSの応答が保たれる
- 各ブロックを切り離すと異常原因を再現・消去できる
- 長時間試験後も電圧、温度、イベント欠落が許容範囲にある

USB HostはINT-01の合格条件ではない。CME H12MIDI Pro等との相互運用は
任意の運用試験とし、未実施または非対応でもRev.Bの電気合格ゲートをFAILに
しない。
