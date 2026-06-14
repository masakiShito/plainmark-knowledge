---
title: "plainmarkで記事とテーマを別リポジトリに分ける理由"
slug: "plainmark-content-repository-strategy"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tech_note"
difficulty: "beginner"
categories:
  - "plainmark"
technologies:
  - "GitHub"
  - "Markdown"
  - "WordPress"
verified_status: "unverified"
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: "plainmark運用設計"
series_order: 1
related_works:
  - "plainmark"
---

# plainmarkで記事とテーマを別リポジトリに分ける理由

## この記事で伝えたいこと

plainmarkでは、テーマ本体と記事・Worksを別リポジトリで管理した方が運用しやすくなります。

テーマは機能開発の履歴、記事は知識更新の履歴です。目的が違うものを同じリポジトリに置くと、あとから変更履歴を追いづらくなります。

## なぜ分けるのか

テーマ本体は、PHP、CSS、テンプレート、管理画面などの実装が中心です。一方で記事やWorksは、日々の学びや成果物の記録です。

たとえば記事を1本追加するたびにテーマリポジトリへコミットすると、以下のような履歴になります。

```text
Fix blog pagination
Add article about React
Add GitHub Works Sync
Update article typo
Add article about AI development
```

これでは、テーマとして何を直したのか、コンテンツとして何を増やしたのかが混ざってしまいます。

## 分けた場合の構成

```text
plainmark
  theme/
  docker-compose.yml
  README.md

plainmark-knowledge
  posts/
  works/
  assets/
  templates/
```

`plainmark` はプロダクト本体、`plainmark-knowledge` は知識の保管場所です。

## メリット

- テーマ開発と記事更新の履歴を分けられる
- MarkdownをGitHub上で管理しやすい
- WordPress側は同期先として扱える
- 記事作成のルールをテンプレート化しやすい
- 将来的に別サイトへ移行しやすい

## 注意点

リポジトリを分けると、同期設定が必要になります。

plainmarkでは、WordPress管理画面の GitHub Pull Sync で以下を設定します。

```text
Owner: masakiShito
Repository name: plainmark-knowledge
Branch: main
Posts path: posts
Works path: works
```

## まとめ

記事とテーマは更新頻度も目的も違います。

そのため、plainmarkを長く運用するなら、テーマ本体とナレッジコンテンツは分けて管理するのが自然です。
