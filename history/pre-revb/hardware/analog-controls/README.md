# ANA-01: アナログ操作

> **Historical:** pre-Rev.B分割検証案です。現行mandatory validationではありません。

## 搭載範囲

- Pitch Bend、CC#1、Velocityの3スライダー
- Emiuet候補の入力RC、GND構成、コネクタ
- 各ADC入力とスライダー端点のテストポイント

## 搭載しないもの

- MCU、電源変換、キー行列、OLED、MIDI出力回路

## 合格の中心

- 全域で単調に変化し、静止時の値が許容幅内に収まる
- Pitch Bendが下端で確実にセンターへ戻る
- キー走査、OLED更新、5V昇圧、USB通信の各条件でノイズを比較する
- フィルタが演奏ジェスチャーを不自然に遅らせない
