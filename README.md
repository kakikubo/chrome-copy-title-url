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

新しいバージョンをインストールするには、上記インストール手順と同じ操作を行います。

1. [Releases](https://github.com/kakikubo/chrome-copy-title-url/releases) から最新の `Chrome-Copy-Title-URL.alfredworkflow` をダウンロード
2. ダウンロードしたファイルをダブルクリック
3. Alfred が同じ Bundle ID の Workflow を検出し、既存の Workflow を上書きインポートします（ホットキーなどの設定は維持されます）

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

## リリース手順

GitHub Actions の **Bump and release** ワークフローで自動化されています。

1. リリースしたい変更を main にマージ
2. Actions タブから **Bump and release** を開き `Run workflow` をクリック
3. `bump_type` で `patch` / `minor` / `major` を選択して実行

`info.plist` の version 更新コミット、`vX.Y.Z` タグ作成、`.alfredworkflow` のビルドと Release 公開まで自動で行われます。

手動でリリースする場合は `info.plist` の `<key>version</key>` をタグと一致させたうえで `git tag vX.Y.Z && git push origin vX.Y.Z` を実行すると、`release.yml` が同等の処理を行います。

## 動作環境

- macOS
- [Alfred](https://www.alfredapp.com/) (Powerpack必須)
- Google Chrome

## License

MIT
