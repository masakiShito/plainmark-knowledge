---
title: "plainmarkの記事front matter設計"
slug: "frontmatter-design-for-plainmark"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tech_note"
difficulty: "beginner"
categories:
  - "Markdown"
technologies:
  - "YAML"
  - "Markdown"
  - "WordPress"
verified_status: "unverified"
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: "plainmark運用設計"
series_order: 3
related_works:
  - "plainmark"
---

# plainmarkの記事front matter設計

## この記事で伝えたいこと

front matterは、Markdown記事をWordPressの記事として扱うための設定情報です。

本文だけでは表現しづらい分類、難易度、検証状態、シリーズ情報をfront matterで管理します。

## 基本形

```yaml
title: "記事タイトル"
slug: "article-slug"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tech_note"
difficulty: "beginner"
categories:
  - "Markdown"
technologies:
  - "YAML"
verified_status: "unverified"
review_date: "2026-09-14"
```

## titleとslug

`title` は表示名、`slug` はURLや同期時の識別子として使います。

slugは英小文字とハイフンで作ると扱いやすいです。

```yaml
title: "Reactのstateをスナップショットとして理解する"
slug: "react-state-snapshot"
```

## article_type

記事の性質を表します。

- `tech_note`: 技術メモ
- `tutorial`: 手順記事
- `error_solution`: エラー解決
- `learning_log`: 学習ログ
- `review`: レビュー記事

記事タイプがあると、JSON-LDや一覧表示で記事の意味を出し分けやすくなります。

## difficulty

読者の前提知識を表します。

- `beginner`: 初学者向け
- `intermediate`: 基礎を知っている人向け
- `advanced`: 実務判断まで含む記事

## verified_status

記事内のコードや手順の検証状態です。

- `verified`: 動作確認済み
- `unverified`: 未検証
- `deprecated`: 古くなった情報

## まとめ

front matterは、記事を単なるMarkdownではなく、検索・分類・同期・鮮度管理できる知識データにするための土台です。
