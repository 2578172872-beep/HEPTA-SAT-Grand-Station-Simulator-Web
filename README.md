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
