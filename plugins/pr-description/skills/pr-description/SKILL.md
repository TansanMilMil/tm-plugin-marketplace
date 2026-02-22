---
name: pr-description
description: "コード差分からプルリクエストの説明文を生成する"
argument-hint: "[git diff対象 例: main...HEAD]"
allowed-tools: Read, Glob, Grep, Bash, AskUserQuestion
---

# Basic Rules

- 引数が指定されている場合は `git diff $ARGUMENTS` で差分を取得する。
- 引数がない場合は `AskUserQuestion` でレビュー対象（git ref またはステージング差分）をユーザーに確認する。
- プルリクエストの説明文は、人間が読みますので理解しやすいよう要約して下さい。
- 説明文は常に日本語かつフォーマルな丁寧語で出力して下さい。
- 出力した内容はクリップボードにコピーしてください。

# Template

出力時は次のテンプレートにしたがって出力してください

## 🏁 Outline

{...}

## 🔗 References

{...}

## 📝 Description

{...}
