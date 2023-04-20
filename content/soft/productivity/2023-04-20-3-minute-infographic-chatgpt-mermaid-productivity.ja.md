---
title: "3分でインフォグラフィック - ChatGPT + Mermaid で生産性を向上させよう"
url: 3-minute-infographic-chatgpt-mermaid-productivity
# date: 2023-04-19T22:00:00+08:00
date: 2023-04-20T10:00:00+08:00
author: androchentw
type: post
categories:
  - soft
tags: 
  - aigc
  - chatgpt
  - productivity
  - infographic
  - diagram
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-20-3-minute-infographic-chatgpt-mermaid-productivity-cover.ja.png?raw=true
series: productivity
---

## 概要

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-20-3-minute-infographic-chatgpt-mermaid-productivity-cover.ja.png?raw=true">
<p align="center"><sub><sup>
  3分でインフォグラフィック - ChatGPT + Mermaidで生産性を向上させよう
</sup></sub></p>

今日は、私が実際に使用している図解ツールとそれらの組み合わせ方を紹介し、視覚化でロジックを説明するのが好きな方々にお役に立てることを願っています。

実は、diagram-as-code ツールは以前から存在していましたが、ChatGPT がこのタスクをさらに簡単にしてくれます。

今日紹介するツールの特徴：

1. 🌐 ウェブページで無料で利用可能。
2. 🚀 フローチャート、マインドマッ。
3. 📝 Markdown (マークダウン記法) を使用し、エンジニアリングのバックグラウンドがなくても簡単に学べ、バージョン管理に便利。

<!--more-->

## Mermaid とは

> JavaScriptベースの図解およびチャート作成ツールで、Markdown にインスパイアされたテキスト定義を動的に作成および変更できる図をレンダリングします。

公式ウェブサイトで、[Mermaid Live Editor](https://mermaid.live)というオンラインエディタを提供しています。

[Mermaid公式チュートリアルドキュメント](https://mermaid.js.org/syntax/flowchart.html)には、参考にできるさまざまな構文の例があります。おおよそ15種類のチャートを描くことができ、以下のように2つのカテゴリに分けられています：

### 1. フローチャート Flowchart

```md
flowchart LR

A[Hard] -->|Text| B(Round)
B --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

{{< mermaid >}}
flowchart LR

A[Hard] -->|Text| B(Round)
B --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
{{< /mermaid >}}

### 2. タイムライン Timeline

```md
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
```

{{< mermaid >}}
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
{{< /mermaid >}}

### 3. ガントチャート Gantt

```md
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
```

{{< mermaid >}}
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
{{< /mermaid >}}

### 4. 円グラフ Pie chart

```md
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```

{{< mermaid >}}
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
{{< /mermaid >}}

### 5. ユーザージャーニー User Journey

```md
journey
  title My working day
  section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
  section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
```

{{< mermaid >}}
journey
  title My working day
  section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
  section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
{{< /mermaid >}}

### 6. マインドマップ Mindmaps

私は放射状のマインドマップに慣れていないので、 [Markmap](https://markmap.js.org/repl) を使用してマインドマップを作成しています。

### その他 Others

以下については、[公式ドキュメント](https://mermaid.js.org/syntax/flowchart.html)を参照してください：

1. シーケンス図 Sequence Diagram
2. クラス図 Class Diagram
3. 状態図 State Diagram
4. 実体関連(ER)図 Entity-Relationship (ER) Diagram
5. 🔥 Gitgraph
6. C4C図

## ChatGPT + Mermaid の実際の応用

あなたは、Mermaidのマークダウン構文がまだ少し複雑に見えるかもしれないと思うかもしれません。その通りです！だからこそ、ChatGPTに構文テンプレートを生成させることができます。ChatGPTが得意なタスク、例えば生成、要約、翻訳などを選択することをお勧めします。

私の例では、Markmapのマインドマップを使用する方が便利で、Mermaidも同じ原則に従います。だから、わずか3分で以下のことを達成することができます:

1. 🤖 [ChatGPT](https://chat.openai.com/): ChatGPT: Prompt (プロンプト) を使用して必要なコンテンツを生成。
2. 📝 [Mermaid Live Editor](https://mermaid.live/): Mermaidに直接コンテンツを入力して図を生成。
3. 🎉 完了！

たとえば、この記事をまとめたい場合は、次のようなプロンプトを使用できます：

```md
# ChatGPT prompt for markdown
provide summary in bullet point and in markdown codeblock:

# ChatGPT prompt for Mermaid
provide summary mermaid diagram in markdown codeblock:
```

以下のマークダウンを入手して：

```md
- 概要
- Mermaid とは
    1. フローチャート Flowchart
    2. タイムライン Timeline
    3. ガントチャート Gantt
    4. 円グラフ Pie chart
    5. ユーザージャーニー User Journey
    6. マインドマップ Mindmaps
    7. その他 Others
- ChatGPT + Mermaid の実際の応用
- 他のツール
- どう思いますか？
```

それを [Markmap](https://markmap.js.org/repl) に貼り付けてマインドマップを生成し、この記事のカバー画像になります。

Mermaidバージョンは、フローチャートを使用して、私のスタイルにより適合しています：

```md
graph LR
    A[概要] --> B[Mermaid とは];
    B --> C[フローチャート Flowchart];
    B --> D[タイムライン Timeline];
    B --> E[ガントチャート Gantt];
    B --> F[円グラフ Pie chart];
    B --> G[ユーザージャーニー User Journey];
    B --> H[マインドマップ Mindmaps];
    B --> I[その他 Others];
    A --> J[ChatGPT + Mermaid の実際の応用];
    A --> K[他のツール];
    A --> L[どう思いますか?];
```

{{< mermaid >}}
graph LR
    A[概要] --> B[Mermaid とは];
    B --> C[フローチャート Flowchart];
    B --> D[タイムライン Timeline];
    B --> E[ガントチャート Gantt];
    B --> F[円グラフ Pie chart];
    B --> G[ユーザージャーニー User Journey];
    B --> H[マインドマップ Mindmaps];
    B --> I[その他 Others];
    A --> J[ChatGPT + Mermaid の実際の応用];
    A --> K[他のツール];
    A --> L[どう思いますか?];
{{< /mermaid >}}

ちなみに、GPT-3.5で生成されたMermaidの結果は、GPT-4で生成されたものよりも優れている理由がわかりません。経験がある方は、ぜひコメントで共有してください〜

## 他のツール

1. [Miro](https://miro.com/): より高度にカスタマイズされたブロック図や他のチャートを描画したい場合は、Miroを優先的に使用します。大きなホワイトボードが大好きで、多くのドラフトアイデアを最終版と一緒に置くことができます。
2. [diagrams.net (旧称 draw.io)](https://app.diagrams.net/): 実際にはdiagrams.netに名前が変更されましたが、みんながまだDraw.ioと呼んでいます。完成したアーキテクチャ図を描く際に、多くの組み込みコンポーネントが利用できることが利点です。しかし、コンポーネントをドラッグして整列させるのはかなり痛いものがあります...。
3. [Excalidraw](https://excalidraw.com/): 手書き風の図解ツール。しばらく使用してから Miro に切り替えました。
4. [PlantUML](https://plantuml.com/): Mermaid と比較されることが多いツール。よりクラシックなインターフェースが特徴です。以前は使用していましたが、今はあまり使っていません。
5. VS Code Plugin
   1. [Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid)
   2. [Markmap](https://marketplace.visualstudio.com/items?itemName=gera2ld.markmap-vscode)

## どう思いますか？

みんなで考えを議論しましょう！🥳

### Murmur

* 2023-04-22: Everything as Code 信じています 🤣
