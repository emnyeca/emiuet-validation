# Rev.B Validation Matrix

## V0 — Power / MCU

| ID | 試験 | 合格条件 |
|---|---|---|
| V0-01 | visual/short check | 極性・部品向きに異常がなく、5V/3V3-GNDに短絡なし |
| V0-02 | current-limited first power | 異常発熱・過電流なし、TP_5V/TP_3V3が設計範囲内 |
| V0-03 | physical power switch | OFFで基板停止、ONで確実に起動し、逆給電なし |
| V0-04 | EN/reset/BOOT | reset、download boot、通常bootが再現可能 |
| V0-05 | flashing/rewrite/recovery | 初回書込み、再書込み、bad firmware後のdownload boot recoveryが可能 |
| V0-06 | repeated power cycle | 20回のOFF/ONでboot失敗・latch・異常発熱なし |
| V0-07 | pilot LED | boot/diagnostic stateをGPIOで表示可能 |

## V1 — Core I/O

| ID | 試験 | 合格条件 |
|---|---|---|
| V1-01 | USB composite | USB MIDI + HID Keyboardとして安定列挙し、抜差し後に再列挙 |
| V1-02 | USB MIDI TX/RX | Emiuet→PCとPC→EmiuetのNote/CCを双方向で確認 |
| V1-03 | 2×3 matrix | 全6 key、diode direction、debounce、同時押し、MIDI生成を確認 |
| V1-04 | slider ×1 | ADC全域、静止noise、smoothing、MIDI CCを確認 |
| V1-05 | button ×1 | press/release、debounce、firmware actionを確認 |
| V1-06 | OLED I2C | 表示更新を継続し、bus hangなし。module側と基板側pull-upの合成と立上り時間を確認 |
| V1-07 | CC検出 / USB状態 | ケーブル両方向でCC電圧とGPIO37を記録し、Default／1.5A以上の判定を確認。attach/configured/suspendはUSB stackで確認 |
| V1-08 | TRS MIDI OUT | Type-A、31.25 kbit/s、実受信機でNote On/Offを確認 |
| V1-09 | TRS MIDI IN | isolationを維持し、Type-A入力をUARTへ受信、USB/I2Cと同時動作 |

## V2 — RGB / USB power

| ID | 試験 | 合格条件 |
|---|---|---|
| V2-01 | SK6812 chain | 6 pixelのRGB order、個別色、DIN/DOUT chainを確認 |
| V2-02 | RMT/DMA | bit-bangなしで更新し、USB/MIDI処理中もframe corruptionなし |
| V2-03 | MIDI RX → RGB | 製品仕様で定義済みのNote On/Off表示を確認。標準CCを未定義のbrightness/mode設定に転用しない |
| V2-04 | current advertisement | Default、1.5A、3Aのsourceを個別に試し、検出はDefault／1.5A以上の二値。Rp低下から消費電流低下まで60 ms以内か波形で測定。3Aでも上限は増やさない |
| V2-05 | Default mode budget | configured、未configured、suspendごとにUSB入力の総電流を測る。RGB黒表示でも残るMCU/OLED/pixel待機電流を含め、状態別USB制限を照合。列挙成功だけで合格にしない |
| V2-06 | 1.5A mode budget | 設定上限内のanimationで5V/3V3、buffer波形、温度が許容範囲 |
| V2-07 | reconnect under animation | animation中のUSB抜差しでreset loop、stale state、hangなし |

## V3 — Rev.B Integrated Prototype

| ID | 試験 | 合格条件 |
|---|---|---|
| V3-01 | all inputs | 78 keys、slider ×3、button ×3、OLED、TRSを同時操作可能 |
| V3-02 | 78 RGB | 全pixel、logical/physical mapping、brightness制限が正しい |
| V3-03 | 5V distribution | 遠端電圧降下、最大/typical current、connector/trace温度を実測 |
| V3-04 | USB MIDI/HID | TX/RX、TYPE mode、抜差し、再列挙、stuck note/keyなし |
| V3-05 | TRS MIDI | IN/OUTをUSBと同時使用して欠落・UART conflictなし |
| V3-06 | integrated load | animation、matrix scan、OLED更新、MIDI traffic同時でも安定 |
| V3-07 | endurance | typical sceneで1～2時間連続動作し、reset・hang・異常温度なし |

## 共通記録

結果は [`results/TEMPLATE.md`](results/TEMPLATE.md) を複製し、基板rev、schematic/BOM/firmware commit、電源とadvertised current、ケーブル、Host OS、測定器、期待値、実測値、判定、写真・波形・ログを記録します。実測前の項目をPASSと推定しません。
