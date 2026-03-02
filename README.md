
[torabo-tsuki](https://github.com/sekigon-gonnoc/torabo-tsuki)用のZMKファームウェア(実験用)

torabo-tsuki LP用は[こちら](https://github.com/sekigon-gonnoc/zmk-keyboard-torabo-tsuki-lp/)

通信頻度が上がった分、操作中も待機中も本来のファームウェアより消費電力が2倍になっています

* _centralがついているuf2をトラックボールがついている方に、_peripheralを反対側に書き込んでください
* キーマップはkeymap-editorおよびzmk-studioで編集できます
* ブートローダを起動するにはキーマップに&bootloaderを割り当てておくか、シリアルポートを1200bpsで開いてから閉じてください
