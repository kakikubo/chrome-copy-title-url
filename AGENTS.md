# AGENTS.md

このリポジトリで作業するエージェント（人間 / AI）向けの運用ドキュメントです。

## プロジェクト概要

- Google Chrome のアクティブタブのタイトルと URL をワンキーでクリップボードにコピーする Alfred Workflow
- リポジトリの実体は単一の `info.plist` のみ（Alfred Workflow のバンドル定義ファイル）
- 配布物の `.alfredworkflow` は `info.plist` を zip 圧縮したもの。リポジトリにはコミットせず、GitHub Release のアセットとしてのみ配布する

## バージョニング（SemVer）

`info.plist` の `<key>version</key>` は [Semantic Versioning](https://semver.org/lang/ja/) (`MAJOR.MINOR.PATCH`) で運用します。

| bump   | 使うケース                                                                 |
| ------ | -------------------------------------------------------------------------- |
| patch  | バグ修正、ドキュメント修正、内部的なリファクタリングなど後方互換のある変更 |
| minor  | 新機能の追加、後方互換のある挙動変更                                       |
| major  | 既存ユーザーの設定や挙動を壊す破壊的変更                                   |

### タグと info.plist のフォーマット

- git タグ: `v` プレフィックスあり（例: `v1.2.0`）
- `info.plist` の `version`: 数字のみ（例: `1.2.0`）
- 両者は常に一致させる（不一致だと `release.yml` の検証ステップで CI が落ちます）

## リリース運用フロー

リリースは 2 系統あります。基本は **Bump and release** ワークフロー（推奨）。

### A. Bump and release（推奨・自動）

`.github/workflows/bump-and-release.yml` が `info.plist` の bump からタグ push、Release 公開までを一括で実行します。

1. リリース対象の変更を `main` にマージする
2. GitHub の Actions タブから **Bump and release** を開き `Run workflow` をクリック
3. `bump_type` で `patch` / `minor` / `major` を選択して実行

ワークフローは以下を自動で行います。

- `info.plist` の `version` を SemVer ルールで bump
- `info.plist の version を X.Y.Z に更新` のコミットを `main` に push
- `vX.Y.Z` タグを作成して push
- `.alfredworkflow` をビルドし、Release ノート付きで GitHub Release を公開

### B. 手動リリース

何らかの理由でローカルからリリースしたい場合は、以下を手動で行います。

1. `info.plist` の `<key>version</key>` を新しい値に更新してコミット
2. `git tag vX.Y.Z` でタグを作成し、`git push origin main` と `git push origin vX.Y.Z` を実行
3. タグ push をトリガーに `.github/workflows/release.yml` が起動し、検証・ビルド・Release 公開を実行

`info.plist` の version とタグの値が一致していないと CI が失敗するので注意してください。

## ビルド手順

### Actions ビルド（リリース時）

`release.yml` および `bump-and-release.yml` の `Build .alfredworkflow` ステップで以下を実行しています。

```bash
zip -q "Chrome-Copy-Title-URL.alfredworkflow" info.plist
```

検証ステップとして `plutil -lint info.plist` と `info.plist` の version とタグ一致チェックを行います。

### ローカルビルド（動作確認用）

ローカルで Alfred に取り込んで動作確認したい場合は同じコマンドで `.alfredworkflow` を作れます。

```bash
plutil -lint info.plist
zip -q "Chrome-Copy-Title-URL.alfredworkflow" info.plist
```

生成された `Chrome-Copy-Title-URL.alfredworkflow` をダブルクリックすると Alfred にインポートできます。**生成物はコミットしないでください**（`.alfredworkflow` は `.gitignore` 対象）。

## CI / ワークフロー一覧

| ファイル                                  | トリガー                  | 役割                                                       |
| ----------------------------------------- | ------------------------- | ---------------------------------------------------------- |
| `.github/workflows/bump-and-release.yml`  | `workflow_dispatch`       | version bump → コミット → タグ push → Release 公開を一括実行 |
| `.github/workflows/release.yml`           | `push` (`v*.*.*` タグ)    | plist 検証、`.alfredworkflow` ビルド、Release 公開         |
| `.github/workflows/release-drafter.yml`   | `push` (`main`) など      | リリースノートのドラフト更新                               |
