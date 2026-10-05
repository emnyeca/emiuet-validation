# VAL-CORE-01 Diagnostic Firmware

製品仕様とtransport/rendering実装は `emnyeca/emiuet/firmware` を正本とし、ここにはVAL-CORE-01固有の診断設定・fixture・ログだけを置きます。

診断buildは起動時にboard ID、hardware rev、firmware commit、reset reason、TUSB320 attach/current/orientationを出力します。USB mount/unmount、matrix、ADC、button、I2C error、MIDI TX/RX、LED frame/current scaleを時刻付きで記録できるようにします。

診断出力の有無で演奏経路を変えず、USB MIDI RX → parser → LED state → RMT rendererは製品firmwareと同じコードを使います。GPIOはVAL-CORE-01回路図を正とし、製品Rev.Bとの差はboard profileで明示します。
