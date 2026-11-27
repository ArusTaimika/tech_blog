---

title: "Gemini・ChatGPT・Claudeのプロンプト書式を公式ガイドから比較する"
emoji: "📝"
type: "tech"
topics: ["生成AI", "ChatGPT", "Gemini", "Claude", "プロンプトエンジニアリング"]
published: false

📌 概要

⚠️ 課題

生成AIに指示を与える際，MarkdownやXML，JSONなど，さまざまな書式が使用されている．

しかし，どのような書式が各生成AIで推奨されているのか，具体的にどのような構造でプロンプトを記述すればよいのかは，意外と知られていない．

そこで今回は，Google，OpenAI，Anthropicの公式ドキュメントを基に，プロンプトの書式について整理する．

💡 結論

各社の公式ドキュメントでは，以下のようなプロンプトの記述方法が紹介されている．

生成AI| 公式ガイドで紹介されている書式| 特徴
Gemini| Markdown・XML| 書式の一貫性
ChatGPT| Markdown＋XML| 情報の階層化と境界の明確化
Claude| XML| タグによる情報の分離

共通しているのは，指示・背景・入力データなどを明確に分離することである．

:::message
本記事は，各社の公式API向けドキュメントを基に整理したものである．書式別の回答精度や処理速度などの比較実験は実施していない．
:::

1. 背景・目的

生成AIへのプロンプトは，自然言語のみでも記述可能である．

しかし，複数の指示や制約条件，参考資料などを入力する場合には，それぞれの情報を明確に区別する必要がある．

例えば，以下のようなプロンプトを考える．

あなたはPythonの専門家です．
与えられたコードをレビューしてください．
外部ライブラリは使用しないでください．
問題点と修正案を日本語で回答してください．

このプロンプトには，以下の要素が含まれている．

要素| 内容
Role| AIの役割
Task| 実行するタスク
Constraints| 制約条件
Output Format| 出力形式

これらを見出しやタグなどで区切ることで，プロンプトの構造を明示できる．

2. プロンプトの代表的な書式

2.1. Markdown形式

Markdownは，見出しや箇条書きなどを用いて文章を構造化する記述形式である．

# Role
Pythonの専門家

# Task
入力されたコードをレビューする．

# Constraints
- 外部ライブラリを使用しない．
- Python 3.11以降を対象とする．

# Output Format
- 問題点
- 修正案
- 修正後のコード

Markdownでは，見出しによって各項目を分類し，箇条書きによって複数の条件を記述できる．

また，"#"，"##"，"###"などを使用することで，情報の階層構造を表現できる．

2.2. XML形式

XML（Extensible Markup Language）は，タグを用いてデータを構造化する記述形式である．

<role>
Pythonの専門家
</role>

<task>
入力されたコードをレビューする．
</task>

<constraints>
- 外部ライブラリを使用しない．
- Python 3.11以降を対象とする．
</constraints>

<output_format>
- 問題点
- 修正案
- 修正後のコード
</output_format>

Markdownとの違いは，開始タグと終了タグによって，各情報の範囲を明示できる点である．

また，タグを入れ子にすることで，階層構造も表現できる．

<documents>
    <document id="1">
        参考資料A
    </document>

    <document id="2">
        参考資料B
    </document>
</documents>

:::message
生成AIへのプロンプトでは，厳密なXML文書ではなく，XML風のタグによる記述も使用されている．
:::

2.3. JSON形式

JSON（JavaScript Object Notation）は，キーと値の組み合わせによってデータを構造化する記述形式である．

{
    "role": "Pythonの専門家",
    "task": "入力されたコードをレビューする",
    "constraints": [
        "外部ライブラリを使用しない",
        "Python 3.11以降を対象とする"
    ],
    "output_format": [
        "問題点",
        "修正案",
        "修正後のコード"
    ]
}

JSONでは，文字列，数値，配列，オブジェクトなどのデータ型を使用できる．

Pythonなどのプログラムからデータを読み込み，プロンプトの内容を変更することも可能である．

2.4. YAML形式

YAMLは，インデントなどを利用して構造化されたデータを記述する形式である．

role: Pythonの専門家

task: 入力されたコードをレビューする

constraints:
  - 外部ライブラリを使用しない
  - Python 3.11以降を対象とする

output_format:
  - 問題点
  - 修正案
  - 修正後のコード

JSONと同様に，キーと値や階層構造を表現できるが，波括弧などを使用せずに記述することも可能である．

2.5. 各書式の比較

項目| Markdown| XML| JSON| YAML
主な構造| 見出し| タグ| キーと値| キーと値
階層表現| 見出しレベル| タグの入れ子| オブジェクト| インデント
情報の区切り| 見出し| 開始・終了タグ| 括弧など| インデント
データ型| なし| スキーマ等で定義可能| あり| あり
主な用途| 文書記述| 構造化文書| データ交換| 設定ファイル等

なお，この表は各書式自体の仕様や特徴を比較したものであり，生成AIにおける性能の優劣を示すものではない．

3. 生成AI別の推奨プロンプト

3.1. Gemini（Google）

Googleの公式ドキュメント「Prompt design strategies」では，Gemini 3向けの設計原則として，Markdownの見出しやXML風のタグを使用する方法が紹介されている．

主な記載内容は以下のとおりである．

- 明確かつ直接的な指示を記述する．
- MarkdownまたはXMLを使用し，プロンプト内で書式を統一する．
- 曖昧な用語やパラメータを明確に定義する．
- 重要な制約条件や役割，出力形式を先頭付近に配置する．
- 大量の参考資料を与える場合は，具体的な質問を最後に配置する．

プロンプトの記述例

<role>
Pythonの専門家
</role>

<constraints>
- 外部ライブラリを使用しない．
- Python 3.11以降を対象とする．
</constraints>

<output_format>
1. 問題点
2. 修正案
3. 修正後のコード
</output_format>

<context>
ここにレビュー対象のコードを記載する．
</context>

<task>
上記のコードをレビューする．
</task>

この例では，役割や制約条件を先頭に配置し，入力データの後に具体的なタスクを記述している．

:::message
Googleの公式ガイドにおける上記の設計原則は，Gemini 3向けとして記載されている．Gemini 4固有の書式として推奨されていることや，書式別の性能については，本記事では確認できていない．
:::

参考資料

https://ai.google.dev/gemini-api/docs/prompting-strategies

3.2. ChatGPT（OpenAI）

OpenAIの公式ドキュメント「Prompt engineering」では，MarkdownとXMLを組み合わせることで，プロンプト内の情報の境界を明確にする方法が紹介されている．

それぞれの書式の用途は以下のとおりである．

書式| 用途
Markdown| 項目の分類・階層構造の表現
XML| 参考資料などの開始位置・終了位置の明示
XML属性| 入力データのメタデータの記述

また，APIのdeveloperメッセージについて，以下の構成が一般的な例として紹介されている．

項目| 内容
Identity| AIの役割・目的・応答スタイル
Instructions| 実行内容・遵守すべき規則
Examples| 入力と期待する回答の具体例
Context| 参考資料・追加情報

プロンプトの記述例

# Identity
Pythonの専門家

# Instructions
入力されたコードをレビューする．

## Constraints
- 外部ライブラリを使用しない．
- Python 3.11以降を対象とする．

## Output Format
1. 問題点
2. 修正案
3. 修正後のコード

# Context
<source_code>
ここにレビュー対象のコードを記載する．
</source_code>

Markdownでプロンプト全体の構造を表現し，XMLタグで入力データの範囲を明示している．

参考資料

https://developers.openai.com/api/docs/guides/prompt-engineering

3.3. Claude（Anthropic）

Anthropicの公式ドキュメント「Prompting best practices」では，複雑なプロンプトをXMLタグによって構造化する方法が紹介されている．

主な記載内容は以下のとおりである．

- 指示，背景，入力データ，回答例を個別のタグで囲む．
- 内容を表す一貫したタグ名を使用する．
- 階層構造が存在する場合はタグを入れ子にする．
- 指示の背景や理由を説明する．
- 期待する回答の具体例を提示する．

プロンプトの記述例

<role>
Pythonの専門家
</role>

<context>
既存のPythonプログラムの保守性を
向上させるためにレビューを実施する．
</context>

<instructions>
入力されたコードをレビューする．
</instructions>

<constraints>
- 外部ライブラリを使用しない．
- Python 3.11以降を対象とする．
</constraints>

<input>
ここにレビュー対象のコードを記載する．
</input>

<output_format>
1. 問題点
2. 修正案
3. 修正後のコード
</output_format>

また，複数の回答例を与える場合には，以下のようにタグを入れ子にする方法が紹介されている．

<examples>
    <example>
        <input>入力例1</input>
        <output>期待する回答1</output>
    </example>

    <example>
        <input>入力例2</input>
        <output>期待する回答2</output>
    </example>
</examples>

長文資料を扱う場合には，資料を質問や指示よりも前に配置する方法も紹介されている．

参考資料

https://platform.claude.com/docs/ja/build-with-claude/prompt-engineering/claude-prompting-best-practices

4. 各社の公式ガイドの比較

項目| Gemini 3向けガイド| OpenAI| Claude
Markdown| 推奨| 推奨| ―
XML| 推奨| 推奨| 推奨
MarkdownとXMLの併用| 書式の統一を推奨| 併用を紹介| ―
役割の指定| 記載あり| 記載あり| 記載あり
回答例の提示| 記載あり| 記載あり| 記載あり
参考資料の配置| 具体的な質問より前| 一般的なdeveloperメッセージでは末尾付近| 長文資料は先頭付近

※「―」は，本記事で参照した書式に関する推奨事項において，明示的な推奨として取り上げていないことを示す．利用できないという意味ではない．

また，各社の公式ガイドは，必ずしも同一の入力条件やAPIメッセージを対象としているわけではない．

5. プロンプトの構造化

各社の公式ドキュメントに登場する主な構成要素を以下に整理する．

項目| 内容
Role / Identity| AIの役割・専門性
Instructions| 実行する内容
Constraints| 制約条件
Context| 背景・参考情報
Input| 処理対象のデータ
Examples| 回答例
Output Format| 出力形式
Task| 具体的なタスク

以下は，これらの構成要素を使用したXML形式の記述例である．

<role>
AIの役割
</role>

<instructions>
具体的な指示
</instructions>

<constraints>
制約条件
</constraints>

<output_format>
期待する回答形式
</output_format>

<examples>
回答例
</examples>

<context>
背景・参考情報
</context>

<input>
処理対象のデータ
</input>

<task>
今回実行するタスク
</task>

:::message
上記は公式ガイドに登場する構成要素を整理した記述例である．3社が共通で定めている標準フォーマットではなく，すべての項目が必須というわけでもない．
:::

6. まとめ

今回は，Google，OpenAI，Anthropicの公式ドキュメントを基に，プロンプトの書式について整理した．

- Gemini：MarkdownまたはXMLを使用し，書式を統一する方法が紹介されている．
- ChatGPT：MarkdownとXMLを組み合わせ，情報の階層と境界を明確にする方法が紹介されている．
- Claude：XMLタグを使用し，指示・背景・回答例・入力データを分離する方法が紹介されている．

各社の公式ドキュメントでは，推奨する書式に違いがあるものの，プロンプト内の情報を明確に区分する方法が共通して紹介されている．

なお，本記事で取り上げた公式ガイドからは，特定の書式がすべてのタスクにおいて最も高い性能を示すとは断定できない．

📚 参考資料

Google

https://ai.google.dev/gemini-api/docs/prompting-strategies

OpenAI

https://developers.openai.com/api/docs/guides/prompt-engineering

Anthropic

https://platform.claude.com/docs/ja/build-with-claude/prompt-engineering/claude-prompting-best-practices

各書式の仕様

https://commonmark.org/

https://www.w3.org/TR/xml/

https://www.json.org/

https://yaml.org/spec/

公式プロンプトガイド確認日：2026年11月27日