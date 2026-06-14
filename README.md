# plainmark-knowledge

plainmark-knowledge は、plainmarkで同期・管理する記事、Works、学習ログをMarkdownで蓄積するためのナレッジリポジトリです。

テーマ本体である `plainmark` とは分離し、コンテンツ更新とテーマ開発の履歴を分けて管理します。

## ディレクトリ構成

```text
plainmark-knowledge/
  posts/      # Blog記事Markdown
  works/      # Works / Portfolio Markdown
  assets/     # 画像などの添付ファイル
  templates/  # 記事・Works作成用テンプレート
```

## WordPress側の同期設定

WordPress管理画面 → ツール → GitHub Pull Sync で以下を設定します。

```text
Owner: masakiShito
Repository name: plainmark-knowledge
Branch: main
Posts path: posts
Works path: works
```

## 記事を書く流れ

1. `templates/article-template.md` をコピーする
2. `posts/` 配下に `slug.md` として保存する
3. front matter を埋める
4. 本文を書く
5. GitHubへpushする
6. WordPress管理画面から GitHub Pull Sync を実行する

## 記事の基本方針

plainmarkの記事は「読んだ人があとで使える知識」にすることを重視します。

- 結論を先に書く
- なぜそう考えたかを書く
- 実装や判断の背景を書く
- つまずいた点を書く
- 動作確認状態とレビュー日を残す
- 関連するWorksがあれば紐付ける

## front matterの主な項目

```yaml
title: "記事タイトル"
slug: "article-slug"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tech_note"
difficulty: "beginner"
categories:
  - "React"
technologies:
  - "React"
  - "JavaScript"
verified_status: "unverified"
review_date: "2026-09-14"
series_name: ""
series_order: 1
related_works: []
```

詳細は `templates/frontmatter-reference.md` を参照してください。
