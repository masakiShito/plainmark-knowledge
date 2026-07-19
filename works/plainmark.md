---
title: "plainmark — 技術記事を公開して終わりにしないWordPressテーマ"
slug: "plainmark"
post_type: "portfolio"
status: "publish"
date: "2026-07-19"
excerpt: "技術記事の検証状態やレビュー期限を管理し、BlogとWorksをつなぐWordPressテーマです。"
work_type: "product"
work_status: "in_progress"
work_summary: "技術記事の公開後まで見据え、検証状態・レビュー期限・依存関係を管理できるWordPressテーマです。"
work_problem: "技術記事は公開時点では正しくても、時間の経過とともにライブラリや実行環境が変わります。通常のブログでは、いつ・どの環境で確認したのかが分かりにくく、古い情報が残り続ける課題がありました。"
work_solution: "記事の検証状態、最終確認日、レビュー期限、依存ライブラリをメタデータとして管理し、Freshness Scoreや要レビュー表示へ反映します。さらにBlogとWorksを相互に関連付け、知識と成果物を同じサイト内でたどれるようにしました。"
work_architecture: "表示を担当するWordPressテーマと、投稿タイプ・メタデータ・Markdown同期などの永続機能を担当するplainmark-coreプラグインを分離しています。記事とWorksはGitHub上のMarkdownを正とし、WordPress側から取得するPull Syncにも対応しています。"
work_features: "記事の検証状態とレビュー期限 / Freshness Score / npm・PyPI依存確認 / BlogとWorksの双方向リンク / Knowledge Map / Learning Paths / Skillsページ / Code Playground / Markdown Pull・Push Sync"
work_learnings: "WordPress開発では画面だけでなく、投稿データの寿命、テーマとプラグインの責務分担、共有サーバーの制約まで含めた運用設計が重要だと学びました。"
work_next_steps: "回帰テストの拡充、Code Playgroundのセキュリティレビュー、Knowledge Mapの実データ検証、互換コードの整理、安定版リリースに向けた配布方法の整備を進めます。"
work_role: "個人開発 / 企画・設計・実装・検証"
work_period: "2026年〜開発中"
work_github_url: "https://github.com/masakiShito/plainmark"
work_demo_url: "https://morofujisan.com/blog/"
technologies:
  - "WordPress"
  - "PHP"
  - "JavaScript"
  - "CSS"
  - "Docker"
  - "GitHub Actions"
  - "Markdown"
related_posts:
  - "wordpress-markdown-sync-design"
---

plainmarkは、技術記事を公開して終わりにせず、公開後の検証・見直し・更新まで管理するためのWordPressテーマです。

記事の検証状態やレビュー期限を可視化し、古くなった情報へ気づける仕組みを用意しています。また、技術記事とWorksを相互に関連付けることで、学んだ知識がどの成果物へつながったのかを確認できるポートフォリオを目指しています。

現在はベータ版として開発中で、WordPressテーマ、plainmark-coreプラグイン、GitHub管理のMarkdownコンテンツを分離して運用しています。