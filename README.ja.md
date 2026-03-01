# AstrBot RSS Forwarder（日本語）

[中文](./README.md) | [English](./README.en.md)

AstrBot RSS Forwarder は、複数の RSS / RSSHub フィードを定期取得し、指定したチャット（グループ/チャンネル/DM）へ自動配信する AstrBot プラグインです。

## 主な機能

- 複数フィード対応（フィード単位で有効/無効）。
- 認証モード：`none` / `query` / `header`。
- ジョブ単位の配信ルーティング（複数 feed + 複数 target）。
- 定期実行：`interval_seconds` 実装済み、`cron` は将来拡張用（現状は interval フォールバック）。
- 重複排除・ETag/Last-Modified 永続化。
- 管理コマンド：`/rss list` / `/rss status` / `/rss run` / `/rss pause` / `/rss resume`。
- LLM 拡張ポイント（失敗時は自動フォールバック）。

## 設定

`_conf_schema.json` により、AstrBot のプラグイン管理画面から主要項目を編集できます（`targets[].unified_msg_origin` は必須）。

## 環境依存関係

### 必須（AstrBot 標準環境で動作）

コア機能は Python 標準ライブラリ + AstrBot API のみを使用するため、通常の RSS 転送では追加の Python パッケージは不要です。

- 推奨 AstrBot バージョン: `>= 4.18.3`
- Python バージョン: AstrBot 実行環境に準拠（通常 `3.10+`）

### 任意機能で必要な準備（ユーザー側で用意）

- `render_mode = image`: AstrBot の HTML→画像実行環境（`html_render`）が必要。
- `llm_enabled = true`: AstrBot 側で LLM Provider 設定が必要。

### インストールエラーについて

`No module named 'commands'` が出る場合、プラグインのパッケージ構成/インポート方法に問題がある可能性があります。
本リポジトリは相対インポート（`from .commands import ...`）と `__init__.py` を含む構成に修正済みです。
