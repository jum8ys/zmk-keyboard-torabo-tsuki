
[torabo-tsuki](https://github.com/sekigon-gonnoc/torabo-tsuki)用のZMKファームウェア(実験用)

torabo-tsuki LP用は[こちら](https://github.com/sekigon-gonnoc/zmk-keyboard-torabo-tsuki-lp/)

通信頻度が上がった分、操作中も待機中も本来のファームウェアより消費電力が2倍になっています

* _centralがついているuf2をトラックボールがついている方に、_peripheralを反対側に書き込んでください
* キーマップはkeymap-editorおよびzmk-studioで編集できます
* ブートローダを起動するにはキーマップに&bootloaderを割り当てておくか、シリアルポートを1200bpsで開いてから閉じてください

## Keymap

<img src="keymap-drawer/torabo-tsuki-s.svg" alt="torabo-tsuki-s keymap" />

## ブートローダの起動方法 (macOS)

### ZMK ファームウェアを書き込んだ後

シリアルポートを1200bpsで開いて閉じるとブートローダが起動する。

1. デバイス名を確認 (`tty.usbmodemXXXXXXX` のような名前)

   ```sh
   ls /dev/tty.usb*
   ```

2. `screen` で1200bpsで開く

   ```sh
   screen /dev/tty.usbmodemXXXXXXX 1200
   ```

3. `Ctrl + a` に続けて `k` を押し、確認プロンプトで `y` を入力して `screen` を終了する。シリアルポートが閉じられるとブートローダが起動する。

### BMP ファームウェアの場合

BLE Micro Pro (BMP) ファームウェアは USB CDC ACM 経由で CLI を公開しており、`dfu` コマンドを送ることでブートローダに遷移させられる（参考: [BMP CLI ドキュメント](https://sekigon-gonnoc.github.io/BLE-Micro-Pro/#/cli)）。`cu` はシリアルポートに対話的に接続するための macOS 標準コマンドで、ポートのロックファイル作成のために `sudo` が必要。

1. デバイス名を確認

   ```sh
   ls /dev/tty.usb*
   ```

2. `cu` でシリアルポートに接続

   ```sh
   sudo cu -l /dev/tty.usbmodemXXXXXXX
   ```

3. プロンプトに対して `dfu` と入力して Enter を押すとブートローダが起動する。

## 補足: 左右間のペアリングがうまくいかない場合

`settings_reset-ble_micro_pro-zmk.uf2` を書き込むことで解消することがある。

> [!WARNING]
> `settings_reset-ble_micro_pro-zmk.uf2` を書き込むと USB 接続でマイコンが認識されなくなる。再度ファームウェアを書き込むには、マイコンの BOOT と GND をショートしたまま USB を接続してブートローダを起動する必要がある。
