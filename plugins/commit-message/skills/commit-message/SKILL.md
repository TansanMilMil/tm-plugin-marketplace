---
name: commit-message
description: "ステージされたgit diffから適切なコミットメッセージを生成する"
argument-hint: "[en] (省略時は日本語で生成)"
allowed-tools: Bash
---

# Rules

- `git diff --staged` を実行してステージ済みの差分を取得してください。
- ステージされた変更がなければ「ステージされた変更がありません。`git add` でファイルをステージしてください。」と通知して終了してください。
- 差分を分析して Conventional Commits 形式のコミットメッセージを生成してください。
- `$ARGUMENTS` が `en` の場合は英語、それ以外は日本語でメッセージを生成してください。

# Commit Message Format

```
<type>(<scope>): <subject>

<body（任意）>
```

# Type 一覧

- `feat`: 新機能
- `fix`: バグ修正
- `docs`: ドキュメントのみの変更
- `style`: コードの意味に影響しない変更（空白、フォーマット等）
- `refactor`: バグ修正・機能追加を伴わないコード変更
- `test`: テストの追加・修正
- `chore`: ビルドプロセス・補助ツールの変更
- `perf`: パフォーマンス改善
- `ci`: CI設定の変更
- `build`: ビルドシステム・外部依存の変更

# Output

- 生成したコミットメッセージをコードブロックで表示してください。
