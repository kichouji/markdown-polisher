# CLAUDE.md

このファイルは Claude Code がこのリポジトリで作業する際の指針です。

## プロジェクト概要

Google ドキュメントから Markdown に変換したテキストを整形する、ブラウザ完結型の静的 Web アプリケーション。

- **技術スタック**: HTML / CSS / Vanilla JavaScript（ライブラリ・フレームワークなし）
- **エントリポイント**: `index.html`（1ファイルで完結）
- **デプロイ先**: GitHub Pages（静的ホスティング）

## ファイル構成

```
index.html        # アプリ本体。HTML・CSS・JS をすべてこの1ファイルに記述する
requirements.txt  # 要件定義書（仕様の根拠として参照する）
sample_latex.txt  # 左ペイン用サンプル入力
sample_image.md   # 右ペイン用サンプル入力
README.md         # プロジェクト説明
CLAUDE.md         # このファイル
```

## 開発ルール

### 基本方針
- **サーバーサイド処理を追加しない**。ブラウザのみで完結させる。
- **外部ライブラリを追加しない**。Vanilla JS で実装する。
- `index.html` の1ファイル構成を維持する（HTML・CSS・JS を分割しない）。

### JavaScript
- `'use strict'` を使用する。
- 各変換機能は独立した関数として実装する（`convertImageTags`, `deleteBase64` など）。
- 変換処理の実行順序は `requirements.txt` の「推奨処理順序」に従う。

### 変換機能の仕様
仕様の詳細は `requirements.txt` を参照すること。概要は以下の通り。

| # | 関数名 | 処理内容 |
|---|---|---|
| 1 | `convertImageTags` | `![][imageX]` を LaTeX 式で置換 |
| 2 | `deleteBase64` | `[imageX]: <data:image/...>` 行を削除 |
| 3 | `deleteAnnotations` | 本文中の注釈番号（`\d{1,2}` + `。`）を削除 |
| 4 | `deleteTrailingSpaces` | 行末の半角スペース・タブを削除 |
| 5 | `insertListSpacing` | リスト項目間に空行を挿入 |
| 6 | `insertListBr` | リスト末尾（最終項目以外）に `<br><br>` を追加 |

### git
- コミットメッセージは日本語で記述する。
- `user.name`: `kichouji`
- `user.email`: `ryu1222@gmail.com`

## サンプルファイルの使い方

- `sample_latex.txt` → 左ペインに貼り付けて動作確認する
- `sample_image.md` → 右ペインに貼り付けて動作確認する
- 両ファイルの LaTeX 式数と `![][imageX]` タグ数は一致している
