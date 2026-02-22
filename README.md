# tm-plugin-marketplace

Claude Code チーム用 skill のプラグインマーケットプレイスリポジトリ。

## インストール方法

### 1. マーケットプレイスを追加

```shell
/plugin marketplace add d002376/tm-plugin-marketplace
```

### 2. スキルをインストール

```shell
/plugin install commit@tm-plugins
/plugin install commit-message@tm-plugins
/plugin install review-performance@tm-plugins
# 他のスキルも同様
```

## 利用可能なスキル

| スキル名 | 説明 |
|---|---|
| `commit` | ステージされた変更をコミット（メッセージ自動生成付き） |
| `commit-message` | ステージされたgit diffから適切なコミットメッセージを生成 |
| `review-code` | コード差分からPRの説明文を生成 |
| `pr-description` | コード差分からプルリクエストの説明文を生成 |
| `generate-class-diagram-java` | Javaクラス/インターフェースの依存関係図をMermaid flowchart記法で生成 |

## ローカルでのテスト

```shell
/plugin marketplace add ./path/to/tm-plugin-marketplace
/plugin install commit@tm-plugins
```

## スキルの同期

`~/.claude/skills/` のスキルをこのリポジトリに同期する場合：

```shell
bash scripts/sync-skills.sh
```

## ディレクトリ構造

```
tm-plugin-marketplace/
├── .claude-plugin/
│   └── marketplace.json    # マーケットプレイスカタログ
├── plugins/
│   ├── <skill-name>/
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   └── skills/<skill-name>/
│   │       ├── SKILL.md
│   │       └── references/  # 一部スキルのみ
└── scripts/
    └── sync-skills.sh      # ~/.claude/skills/ → plugins/ 同期スクリプト
```
