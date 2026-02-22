---
name: generate-class-diagram-java
description: "Javaクラス/インターフェースの依存関係図をMermaid flowchart記法で生成する"
argument-hint: "[クラス名またはパッケージ名]"
allowed-tools: Read, Glob, Grep, Bash, AskUserQuestion
---

## Javaクラス依存関係図生成プロンプト

- 引数が指定されている場合は `$ARGUMENTS` をクラス/インターフェース名として使用してください。
- 引数がない場合は `AskUserQuestion` でどのクラス・パッケージを対象にするか確認してください。
- 対象クラス/インターフェースとその依存関係にある class、interface 同士の関係図を Mermaid flowchart 記法で出力してください。

### 生成時のルール:

1. **パッケージグルーピング**: subgraphを使用してパッケージごとにクラスをグループ化してください
2. **パッケージ名**: `...{重要な部分のみ}`形式で短縮表記（絵文字不要）にする
3. **クラス情報**: 各クラスには以下を表記する
   - クラス名
   - クラス種別: `class`, `interface`, `abstract class`, `enum`, `record`
   - publicメンバーのみ（privateフィールドは除外）
   - メソッド名のみ（戻り値型、引数型は省略）
   - フィールド名のみ（型情報は省略）

4. **関係性**: 以下の関係を表現する
   - 継承: `-.->|extends|`
   - 実装: `-.->|implements|`
   - 依存: `-->|uses|`
   - 構成: `-->|contains|`
   - データフロー: `-->|returns|`, `-->|converts|`, `-->|creates|`

5. **除外対象**: 以下はmermaidの図には一切含めないこと
   - アノテーション（@Service, @Controller等）
   - privateフィールド・メソッド
   - 複雑な型表記（ジェネリクス等は簡略化）

### 調査手順:

1. 指定されたクラスを読み込み
2. そのクラスが依存する全てのクラス・インターフェースを特定
3. 各クラスのパッケージ、継承関係、依存関係を調査
4. flowchartでパッケージごとにグループ化して図式化
