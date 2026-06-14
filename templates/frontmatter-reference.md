# front matter reference

plainmarkで同期するMarkdownは、ファイル先頭にYAML front matterを書きます。

## 記事用

```yaml
title: "記事タイトル"
slug: "article-slug"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tech_note"
difficulty: "beginner"
categories:
  - "カテゴリ名"
technologies:
  - "技術名"
verified_status: "unverified"
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: ""
series_order: 1
related_works: []
```

## Works用

```yaml
title: "Worksタイトル"
slug: "work-slug"
post_type: "portfolio"
status: "publish"
date: "2026-06-14"
work_type: "product"
work_status: "released"
technologies:
  - "技術名"
related_posts: []
```

## article_typeの目安

- `tech_note`: 技術メモ
- `tutorial`: 手順・解説
- `error_solution`: エラー解決
- `learning_log`: 学習ログ
- `review`: 技術やサービスのレビュー
- `portfolio`: Works連動記事

## difficultyの目安

- `beginner`: これから学ぶ人向け
- `intermediate`: 基礎を知っている人向け
- `advanced`: 実務・設計判断まで扱う記事

## verified_statusの目安

- `verified`: 動作確認済み
- `unverified`: 未検証
- `deprecated`: 古くなった、または非推奨
