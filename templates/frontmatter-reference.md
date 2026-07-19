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
date: "2026-07-19"
excerpt: "Works一覧やOGPで使用する短い説明"
work_type: "product"
work_status: "released"
work_summary: "詳細ページ上部に表示する要約"
work_problem: "制作の背景となった課題"
work_solution: "採用した解決方法"
work_architecture: "技術構成や責務分割"
work_features: "主な機能"
work_learnings: "制作を通して学んだこと"
work_next_steps: "今後の改善予定"
work_role: "個人開発 / 設計・実装"
work_period: "2026年"
work_github_url: "https://github.com/owner/repository"
technologies:
  - "技術名"
related_posts: []
```

デモURLがあるWorksだけ、次の項目を追加します。

```yaml
work_demo_url: "https://example.com"
```

Worksの本文は詳細ページの「何を作ったか」セクションへ表示されます。

次の内容は本文に見出しを作らず、専用front matterへ記載します。

- 課題: `work_problem`
- 解決: `work_solution`
- 設計: `work_architecture`
- 主な機能: `work_features`
- 学び: `work_learnings`
- 今後の改善: `work_next_steps`

本文の先頭にH1タイトルは不要です。タイトルはWordPress側で自動表示されます。

現在の簡易YAMLパーサーでは、`|`を使った複数行文字列と、`work_demo_url: ""`のような空文字のオプション項目を正しく扱えません。Worksの専用フィールドは1行で記載し、値がないオプション項目は行ごと省略してください。

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