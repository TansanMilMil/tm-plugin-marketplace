# CLAUDE.md

## このリポジトリについて

`/home/ubuntu/develop/tm-plugin-marketplace` は Claude Code チーム向けスキルのプラグインマーケットプレイスの**参照元データ**リポジトリです。
インストール済みスキルの大元となるデータを管理します。

## 編集対象のルール

- スキルの修正・追加を指示された場合、**このディレクトリ（`/home/ubuntu/develop/tm-plugin-marketplace/plugins/`）を編集対象**としてください。
- `~/.claude/plugins/` 配下のキャッシュや参照コピーは編集しないでください。編集するとしても、このディレクトリを優先してください。

## プラグインのディレクトリ構造

各プラグインは以下の構造で管理します。

```
plugins/
└── <skill-name>/
    ├── .claude-plugin/
    │   └── plugin.json       # プラグインメタデータ
    └── skills/
        └── <skill-name>/
            └── SKILL.md      # スキル本体の定義
```

### plugin.json の必須フィールド

```json
{
  "name": "<skill-name>",
  "description": "スキルの説明",
  "version": "1.0.0"
}
```

### SKILL.md のフロントマター

```yaml
---
name: <skill-name>
description: "スキルの説明"
argument-hint: "[引数の説明 例: main...HEAD]"  # 省略可
allowed-tools: Bash, Read, Glob, Grep, AskUserQuestion, Skill  # 必要なものだけ列挙
---
```

- `argument-hint` は省略可。引数を受け取らないスキルには不要。
- `allowed-tools` はスキルが実際に使うツールのみを列挙する。

## 新規スキル追加手順

1. `plugins/<skill-name>/.claude-plugin/plugin.json` を作成する
2. `plugins/<skill-name>/skills/<skill-name>/SKILL.md` を作成する
3. 必要に応じて `~/.claude/plugins/` へのインストール手順をユーザーに案内する

## スキルのルール

- スキルの SKILL.md を編集した際は、`plugins/<skill-name>/skills/<skill-name>/SKILL.md` を修正してください。

## 既存スキル一覧

| スキル名 | 説明 |
|---|---|
| `commit` | ステージ済み変更をコミットする（`commit-message` を内部で呼び出す） |
| `commit-message` | ステージ済み差分から Conventional Commits 形式のメッセージを生成する |
| `review-code` | コード差分をシニアエンジニア視点でレビューする |
| `pr-description` | コード差分からプルリクエスト説明文を生成する |
| `generate-class-diagram-java` | Javaクラスの依存関係を Mermaid flowchart で図式化する |

### commitスキルの仕様

- `commit` スキルは実行直後（ツール呼び出しより前）に処理開始メッセージを標準出力すること。
  - 理由: `claude -p` によるターミナルのインライン実行で処理開始を即座に確認できるようにするため。
  - 出力内容: `コミット処理を開始します。ステージ済みの差分を確認しています...`
