---
title: "Auto-GPT と AgentGPT はどれほどすごい？ AIが全自動でタスクを完了 - 入門編"
url: auto-gpt-agentgpt-introduction
# date: 2023-04-15T20:30:00+08:00
date: 2023-04-16T09:00:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - aigc
  - chatgpt
  - autogpt
  - agentgpt
  - productivity
  - agile
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-1-architecture.ja.png?raw=true
series: aigc
---

## 概要

<img style="width:100%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-1-architecture.ja.png?raw=true">
<p align="center"><sub><sup>
  Auto-GPT / AgentGPT の 自動 AI メカニズム
</sup></sub></p>

ChatGPT のリリースから約4ヶ月後、AIを使ってタスクを自動的に完了させるアーキテクチャ [Auto-GPT](https://github.com/Torantulino/Auto-GPT) と [AgentGPT](https://agentgpt.reworkd.ai) が登場しました。

つまり、あなたが "**目標 Goal**" を提供すれば、反復的な（**タスクの分解 > 実装 > 検証**）プロセスを経て、最終的に**タスクを自動的に完了させることができます**。

Auto-GPT をこれほどすごいものにする鍵は：

1. 🧠 LLM を使用して要求を理解し、タスクを展開する
2. 🌐 インターネットに接続し、最新情報をリアルタイムで検索できる
3. 💾 ChatGPT トークンの上限を突破する長期記憶ストレージをサポートする

今日は以下の 4 つのポイントから、観察と総括を共有します。

1. 🔥 デモンストレーション
2. ☠️ 注意喚起: 💰 予算管理
3. 👀 要件/審査/フェーズレビューの重要性
4. 🚀  Agile/Lean Startup "MVP" コンセプトを活用して、自分のロケットを作成する

🤔 Q: Auto-GPTはどの程度できるのか？

💪 A: AIを何に使って、どのような効果が得られるのか？さらなる発揮可能性は？

> (2023/04/16) 台湾出身のITエンジニアです 🇹🇼 ChatGPTなどのソフトウェアを使って、オリジナルや今後読む価値のある記事の翻訳を手伝っています。もし分かりにくい表現があれば、遠慮なく教えてください。私も英語と日本語の学習に努力しています！

<!--more-->

## 🔥 モンストレーション

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-2-agentgpt.png?raw=true">
<p align="center"><sub><sup>
  AgentGPT サンプル Web インターフェイス
</sup></sub></p>

私は AgentGPT に "Build modern startup landing page 現代のスタートアップ向けランディングページを作成する" と尋ね、次のタスクが自動的に生成されました。

1. Generate a list of modern landing page designs from popular startup websites (人気のスタートアップWebサイトから現代のランディングページデザインのリストを生成する)
2. Identify key design elements and features that are common among the selected designs (選択されたデザインの中で共通のデザイン要素と機能を特定する)
3. Create a prototype landing page incorporating the identified design elements and features (特定されたデたデザイン要素と機能を取り入れたプロトタイプのランディングページを作成する)

そして最初のタスクから始め、Airbnb、Uber、Spotifyなどの有名なモダンなランディングページデザインのリストを作成しました。細かい部分は最初に考えていたものとは必ずしも一致しないかもしれませんが、問題解決のアプローチとして参考にする価値があると思います。

Auto-GPTとAgentGPTの両方で使用される語彙と手順は異なりますが、大筋では同じです。

* Auto-GPT: Goal -> N Thought > (Reasoning, Criticism > Next Action, System) -> Result
* AgentGPT: Goal -> N Task > (Thinking > Executing) -> Result

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-3-auto-gpt.jpg?raw=true">
<p align="center"><sub><sup>
  Auto-GPT サンプル コマンドインターフェース
</sup></sub></p>

また、[BabyAGI の Task-driven Autonomous Agent](https://twitter.com/yoheinakajima/status/1640934493489070080) は原理を図示しており、[繁体字中国語訳](https://github.com/yoheinakajima/babyagi/blob/main/docs/README-zh-tw.md)を提供するPRも出しました。興味のある方はぜひ参考にしてください。

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-4-babyagi.png?raw=true">
<p align="center"><sub><sup>
  BabyAGI アーキテクチャ原理
</sup></sub></p>

## ☠️ 注意喚起：💰 予算管理

現在、確認できることが一つあります。それは、Auto-GPTが提供する連続モードは、本当に**すぐにクレジットカードの限度額を消費することです**。

ですので、OpenAI APIで予算上限を設定しておくことを忘れないでください。

## 👀 要件/審査/フェーズレビューの重要性

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-5-programmer-joke.ja.jpg?raw=true">
<p align="center"><sub><sup>
  古典的なプログラミング言語のジョーク - スイカを見たら1つ買う、オレンジを見たら10個買う
</sup></sub></p>

これは古典的なプログラミング言語のジョークを思い出させます。

> 妻が夫に言います。「スーパーでスイカを見たら1つ買って、オレンジを見たら10個買ってきてね」。
>
> 結果として、夫は10個のスイカを買いました。
>
> （注釈：夫は「オレンジを見た」ので、スイカを10個買いましたが、妻の要求はオレンジを10個買うことでした）

「**正確な質問**」に加えて、「**正確な要求の説明**」が今後の鍵となります。なぜなら、これは、あなたが10個のスイカを受け取るか、予期しない他の行動を受け取るかどうかに直接影響します。

## 🚀 Agile/Lean Startup "MVP" コンセプトを活用して、自分のロケットを構築する

<img style="width:100%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-6-mvp.jpg?raw=true">
<p align="center"><sub><sup>
  <a href="https://startupbasics.com/minimum-viable-product" target="_blank rel="noopener noreferrer">startup basics</a> - Lean Startup MVP コンセプト スケートボード -> 自動車
</sup></sub></p>

これまでの内容を読んでいただいた方で、Agile software engineering（敏捷性のあるソフトウェア開発）に関連する経験がある方は、きっと馴染みがあると思います。

「**多くの時間とコストをかけて、最終的にはユーザーが必要としていない製品を作る**」ということを避ける方法が、AgileとLean Startupの強みです。

MVP（**Minimum Viable Product、最小限の実行可能な製品**）とは、スケートボードと自動車を例にすると、キーユーザーに製品を提供する際に採用する反復的な方法を指します。

* ❌ やってはいけない: 車輪 > 底盤 > ドア > 自動車
* ✅ やるべき: スケートボード > 自転車 > オートバイ > 自動車

理由は非常にシンプルで、もし顧客が解決したい問題が「歩くのが嫌で、もっと速くて便利な交通手段が欲しい」というものであれば、スケートボードは2週間後に提供できるかもしれません。しかし、自動車は組み立てが完了するまで提供できない部品であり、実際に使えるようになるまで半年かかるかもしれません。その時点で顧客のニーズはすでに変わっているかもしれません。

そこで、Auto-GPTをさまざまな面で活用することができるかもしれません。いくつかの例を挙げます:

1. MVPを設定し、段階的に最小限の目標を設定して成果を確認し、反復を繰り返します。
2. Auto-GPTがタスクを分解する方法を学び、普段のAgile breakdown（エピック > ストーリー > タスク）のプロセスで逆に利用します。

## あなたの意見は？

次回は、自分がAuto-GPTとAgentGPTの間での使用感や評価をシェアする予定です。

どんなアプリケーションが見たいですか？

あなたの考えをコメントして一緒に議論しましょう！🥳

### Murmur

* 2023-04-15: 驚くべき進展の速さ。まさに AIGC 元年ですね 🤣
