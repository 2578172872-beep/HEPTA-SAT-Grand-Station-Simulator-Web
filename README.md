# HEPTA-SAT Grand Station Simulator Web — GitHub Pages

GitHub Pages専用の静的Web版です。

公開予定URL:

```text
https://2578172872-beep.github.io/HEPTA-SAT-Grand-Station-Simulator-Web/
```

## 構成

- `index.html`: 機能選択と画面切替の入口
- `features.js`: 機能一覧
- `app.js`: 機能選択処理
- `styles.css`: 機能選択とプレースホルダーのスタイル
- `public/ground-station.html`: 既存地上局UI
- `public/`: 地図、衛星軌道、Three.js資産
- `.github/workflows/pages.yml`: GitHub Pages自動公開

## 新しい機能を追加する

1. `features.js` に機能情報を追加する。
2. `index.html` に同じIDの `data-feature-view` セクションを追加する。
3. 必要なJavaScriptやCSSを独立ファイルとして追加する。

Ground Stationのiframeは機能切替時も破棄しないため、シリアル接続や画面状態を維持します。

## ローカル確認

ファイルを直接開かず、HTTPサーバーから表示してください。

```bash
python3 -m http.server 8080
```

ChromeまたはEdgeで `http://localhost:8080/` を開きます。

## テレメトリ通信仕様

Web SerialとXBee UARTは参照Flight Softwareと同じ **9600 baud** です。機体側・地上局側XBeeは
`AP=0`（Transparent mode）、`BD=3`（9600 baud）に設定してください。

受信処理はHEPTA-SAT Serial Monitorと同様に、Web Serialの任意の受信チャンクを
改行まで蓄積してから解析します。Lab5-03の
`TEMP=...,BUS=...,V5=...`形式、およびFlightwareの
`V=...,TEMP=...,AX=...`形式に対応しています。実機から到着したデータは、
ベンチ試験でも確認できるよう衛星仰角に関係なく表示します。

23バイトHK Payloadの2バイト値はビッグエンディアンで、次の物理単位を使用します。

- 電圧: ADC count（V ÷ (3.3 × 1.431) × 4096）
- 温度: 0.1 °C
- 加速度: 512 count/g
- 角速度: deg/s × 2048 ÷ 125
- 地磁気: µTの整数値

30バイトのバイナリテレメトリと、Lab5形式の改行区切りテキストテレメトリを
自動判別します。1つの送信方式の途中に別方式を混在させないでください。
