---
title: "AI駆動開発のはじめ方"
slug: "ai-driven-development-first-step"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "learning_log"
difficulty: "beginner"
categories:
  - "AI駆動開発"
technologies:
  - "AI駆動開発"
  - "開発プロセス"
verified_status: "unverified"
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: "AI駆動開発実践入門"
series_order: 1
related_works:
  - "plainmark"
---

# AI駆動開発のはじめ方

## この記事で伝えたいこと

AI駆動開発は、AIに丸投げする開発ではありません。

人間が目的、制約、確認観点を決め、AIを実装や整理の補助として使う開発スタイルです。

## 最初に決めること

AIに依頼する前に、以下を決めます。

- 何を作るのか
- なぜ作るのか
- どこまでを今回作るのか
- 既存コードのどこを触ってよいのか
- 完了条件は何か

ここが曖昧だと、AIの出力も曖昧になります。

## 良い依頼の例

```text
WordPressテーマの管理画面に、GitHubリポジトリ一覧を表示するページを追加したい。
まずはpublic repositoryのみ対応でよい。
既存のportfolio投稿タイプにWorks下書きを作成できるようにしたい。
```

目的、範囲、制約が入っているため、実装に進みやすくなります。

## AIに任せすぎない

AIはコードを書けますが、プロダクトの意図や運用上の判断は人間が持つ必要があります。

特に以下は人間が確認します。

- セキュリティ
- 既存仕様との整合性
- データが壊れないか
- UIが運用しやすいか
- テストや確認方法

## まとめ

AI駆動開発では、AIに何をさせるかよりも、人間が何を決めるかが重要です。

良い前提を渡すほど、AIの出力は実用的になります。
