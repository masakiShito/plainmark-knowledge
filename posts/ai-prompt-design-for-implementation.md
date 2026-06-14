---
title: "実装を依頼するためのAIプロンプト設計"
slug: "ai-prompt-design-for-implementation"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tech_note"
difficulty: "intermediate"
categories:
  - "AI駆動開発"
technologies:
  - "AI駆動開発"
  - "プロンプト設計"
verified_status: "unverified"
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: "AI駆動開発実践入門"
series_order: 2
related_works:
  - "plainmark"
---

# 実装を依頼するためのAIプロンプト設計

## この記事で伝えたいこと

AIに実装を依頼するときは、作業指示だけでなく、前提・制約・確認方法をセットで伝えると安定します。

## プロンプトに入れる要素

実装依頼では、最低限以下を入れます。

```text
目的
現状
変更したいこと
触ってよいファイル
触ってほしくないファイル
完了条件
確認方法
```

## 悪い例

```text
Worksの機能を作って
```

これでは、何をどこまで作るのか分かりません。

## 良い例

```text
WordPress管理画面にGitHub Works Syncページを追加してください。
MVPではGitHub usernameからpublic repositoryを取得し、一覧からportfolio下書きを作成できればよいです。
private repositoryやtoken認証は今回は不要です。
既存のportfolio投稿タイプとwork_*メタ項目を使ってください。
```

このように書くと、AIは既存設計に沿って実装しやすくなります。

## 確認観点も渡す

実装だけでなく、確認観点も渡します。

- 管理画面にメニューが出るか
- nonceチェックがあるか
- 権限チェックがあるか
- 既存Worksと重複作成しないか
- public repoだけで動くか

## まとめ

AIに実装を頼むときは、コードを書かせる前に「判断材料」を渡すことが重要です。

プロンプトは指示文ではなく、開発の設計書として扱うと精度が上がります。
