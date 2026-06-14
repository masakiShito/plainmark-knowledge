---
title: "GitHub Pull Syncの基本フロー"
slug: "github-pull-sync-basic-flow"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tutorial"
difficulty: "beginner"
categories:
  - "plainmark"
technologies:
  - "GitHub"
  - "WordPress"
  - "Markdown"
verified_status: "unverified"
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: "plainmark運用設計"
series_order: 2
related_works:
  - "plainmark"
---

# GitHub Pull Syncの基本フロー

## この記事で伝えたいこと

GitHub Pull Syncは、WordPress側からGitHubのMarkdownを取りに行く仕組みです。

外部からWordPressへPOSTするのではなく、WordPressが自分でGitHub APIを呼び出すため、WAFやサーバー制約の影響を受けにくくなります。

## 基本の流れ

```text
GitHubにMarkdownをpush
↓
WordPress管理画面で同期実行
↓
GitHub APIからMarkdownを取得
↓
front matterを読み取る
↓
投稿またはWorksとして作成・更新
```

## なぜPull型にするのか

GitHub ActionsからWordPressにPOSTする方式だと、サーバーのWAFにブロックされることがあります。

Pull型なら、WordPress自身がGitHubにアクセスするだけなので、受信側の制限を回避しやすくなります。

## 同期対象

plainmark-knowledgeでは、以下を同期対象にします。

```text
posts/  # 記事
works/  # Works
```

WordPress側の設定で、これらのパスを指定します。

## 同期時に見る情報

主に以下を見ます。

- Markdownファイルのパス
- Git blob SHA
- front matter
- slug
- post_type
- status
- technologies

同じSHAのファイルはスキップされるため、変更がない記事を何度も更新しない設計にできます。

## まとめ

GitHub Pull Syncは、GitHubを原本にしながらWordPressの管理画面と表示機能を使うための仕組みです。

plainmarkでは、この仕組みによって「Gitで管理するMarkdown」と「WordPressで見せるサイト」を両立できます。
