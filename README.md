# Chrome Copy Title URL

Google ChromeのアクティブタブのタイトルとURLをワンキーでクリップボードにコピーするAlfred Workflowです。

## 出力形式

```
ページタイトル https://example.com/page
```

ペースト時に `タイトル URL` の形式で出力されます。

## インストール

1. [Releases](https://github.com/kakikubo/chrome-copy-title-url/releases) から最新の `Chrome-Copy-Title-URL.alfredworkflow` をダウンロード
2. ダウンロードしたファイルをダブルクリック
3. Alfredのインポート画面が開くので「Import」をクリック

## アップデート

新しいバージョンの `Chrome-Copy-Title-URL.alfredworkflow` を [Releases](https://github.com/kakikubo/chrome-copy-title-url/releases) からダウンロードし、ダブルクリックすると Alfred が既存のワークフローを上書きインポートします。設定したホットキーは維持されます。

## 使い方

1. Google Chromeでコピーしたいページを開く
2. `Cmd + Ctrl + C` を押す
3. クリップボードにタイトルとURLがコピーされる
4. 「Copied!」の通知が表示される
5. 任意の場所で `Cmd + V` でペースト

## 必要な設定

初回実行時にmacOSからAppleScriptのアクセス許可を求められる場合があります。

**システム設定 > プライバシーとセキュリティ > オートメーション** でAlfredからGoogle Chromeへのアクセスを許可してください。

## ホットキーの変更

`Cmd + Ctrl + C` を変更したい場合は:

1. Alfredの設定を開く
2. Workflows > Chrome Copy Title URL を選択
3. Hotkey Triggerをダブルクリック
4. 好みのキーコンビネーションに変更

## 動作環境

- macOS
- [Alfred](https://www.alfredapp.com/) (Powerpack必須)
- Google Chrome

## License

MIT
