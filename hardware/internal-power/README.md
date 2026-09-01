# PWR-01: Emiuet内蔵電源

Emiuet Rev.Bへ統合する電源回路だけを検証するPCBです。Hearthの回路を
そのまま転用せず、Emiuetの製品条件を正として設計します。

## 搭載範囲

- 充電専用USB-C入力と保護
- 1セルLi-ionコネクタと極性・逆流保護
- PowerPath充電
- Emiuetが必要とする5V/3.3V生成
- BAT_VSENSE、PGOOD、CHG
- 各レールのテストポイント、切り離しジャンパ、段階式ダミー負荷
- USB-C #2を接続したCORE-01との二重USB接続、逆流、電源遷移試験

## 搭載しないもの

- ESP32-S3、USB-C #2 D+/D-、Composite Device firmware
- キー、スライダー、OLED、TRS MIDI
- EUB-BUSを前提とする製品コネクタ

## 製造前に確定する値

- 通常/最大の5V・3.3V負荷
- 充電電流と電池容量・許容温度
- 許容リップルと瞬時電圧降下
- 低電圧時の停止・再起動方針

回路図には全入力状態の電流経路、部品のデータシートURL、設定値の計算を
直接記載します。

USB-C #2は製品仕様上の給電入力ではなく、自己給電USB DeviceのVBUS
presence senseである。PWR-01はデータ信号を扱わないが、USB-C #1と#2の
同時接続、内部レールへの意図しない給電、USB-C #2への逆流をCORE-01との
結合試験で確認する。
