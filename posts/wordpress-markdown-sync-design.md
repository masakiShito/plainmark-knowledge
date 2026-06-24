---
title: Markdownをsource of truthにしてWordPressへ同期する設計メモ
slug: wordpress-markdown-sync-design
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: intermediate
categories:
  - WordPress
technologies:
  - WordPress
  - Markdown
  - GitHub Actions
verified_status: unverified
verified_date: ""
verified_env: WordPress 6.x / Node.js 22 / macOS
review_date: 2026-09-23
ci_status: unknown
ci_checked_at: ""
ci_run_url: ""
tested_path: ""
test_command: ""
related_works:
  - plainmark
---

## はじめに

WordPress の管理画面で直接記事を書くと、レビュー、差分確認、検証、履歴管理が難しくなることがあります。

Markdown ファイルを GitHub で管理し、それを WordPress に同期する形にすると、記事をコードと同じように扱えます。

この記事では、Markdown を source of truth にして WordPress へ同期する設計の基本を整理します。

## 前提

この記事では、次のような構成を想定します。

```text
plainmark-knowledge/
├── posts/
│   └── article-slug.md
├── works/
│   └── work-slug.md
└── assets/
```

記事本文と front matter は GitHub 上の Markdown ファイルを正とします。

## 完成形

運用の流れは次のようになります。

```text
1. Markdown記事を書く
2. Pull Requestを作る
3. CIでfront matterと検証コードを確認する
4. mainにmergeする
5. WordPressへ同期する
```

WordPress 側で直接編集するのではなく、GitHub 上の Markdown を更新します。

## front matterに持たせる情報

記事の先頭に、同期に必要な情報を書きます。

```yaml
title: TypeScriptの型ガードでunknownを安全に扱う
slug: typescript-type-guards
post_type: post
status: draft
date: 2026-06-23
verified_status: unverified
review_date: 2026-09-23
```

最低限、次の情報があると同期しやすくなります。

```text
- title
- slug
- post_type
- status
- date
```

さらに、技術記事では検証状態も持たせると品質管理に役立ちます。

```text
- verified_status
- verified_date
- verified_env
- review_date
- tested_path
- test_command
```

## slugを同期キーにする

WordPress へ同期する場合、何をキーにして既存記事を更新するかを決める必要があります。

扱いやすいのは slug です。

```text
posts/typescript-type-guards.md
slug: typescript-type-guards
WordPress post_name: typescript-type-guards
```

このように揃えると、Markdown ファイルと WordPress 記事の対応が分かりやすくなります。

## statusを管理する

Markdown 側の status を WordPress の投稿ステータスに対応させます。

```yaml
status: draft
```

下書きなら draft、公開するなら publish とします。

ただし、公開操作を自動化する場合は慎重に設計します。最初は draft だけ同期し、WordPress 側で表示確認してから公開する運用でも問題ありません。

## CIで検証する

同期前に CI で検証します。

検証項目の例です。

```text
- front matterの必須項目がある
- slugとファイル名が一致している
- statusが許可された値である
- tested_pathが存在する
- test_commandが成功する
```

検証結果を front matter に書き戻す場合は、同期ワークフローとの責務分離が重要です。

## WordPress同期の考え方

同期処理では、Markdown を次のように変換します。

```text
front matter.title -> post_title
front matter.slug -> post_name
front matter.status -> post_status
Markdown本文 -> post_content
```

カテゴリや技術タグも front matter から同期できます。

```yaml
categories:
  - TypeScript
technologies:
  - React
  - TypeScript
```

WordPress 側では、カテゴリ、タグ、カスタムタクソノミーのどれに対応させるかを事前に決めます。

## よくある詰まりどころ

### WordPress側で直接編集して差分が消える

Markdown を source of truth にする場合、WordPress 側の直接編集は上書きされる可能性があります。

管理画面には、本文は GitHub で管理していることを分かるようにしておくと混乱を減らせます。

### 同期処理と検証処理を混ぜる

同期処理の中で検証まで行うと、失敗時の原因が分かりにくくなります。

CI で検証し、同期は通ったものだけを反映する設計が分かりやすいです。

### slug変更の扱い

slug を変更すると、WordPress 側では別記事として扱われる可能性があります。

公開後の slug 変更は、リダイレクトや既存記事の更新方針を決めてから行います。

## まとめ

Markdown を source of truth にして WordPress へ同期すると、記事管理を GitHub ベースにできます。

重要なのは、front matter の設計、slug の一貫性、CI 検証、同期責務の分離です。

最初は下書き同期から始め、運用が安定してから公開まで自動化するのがおすすめです。
