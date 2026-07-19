---
title: "Wealth Manager — 老後資産を見える化するシミュレーション基盤"
slug: "wealth-manager"
post_type: "portfolio"
status: "publish"
date: "2026-07-19"
excerpt: "現在の資産・収支・積立状況を整理し、老後資産の過不足を試算するためのWebアプリです。"
work_type: "product"
work_status: "in_progress"
work_summary: "現在の資産・収支・積立状況を整理し、将来の老後資産が足りるかを試算するためのWebアプリです。"
work_problem: "老後に必要な金額は、退職年齢、寿命、生活費、年金、現在資産、毎月の積立額によって大きく変わります。情報が複数の口座や家計記録へ分散していると、現状と将来の不足額を一貫して把握しにくい課題がありました。"
work_solution: "資産種別・口座・月次収支を共通のデータモデルで管理し、その情報を将来の老後資産シミュレーションへつなげる構成にしました。まず認証と資産管理の基盤を実装し、計算機能を段階的に追加できる設計にしています。"
work_architecture: "フロントエンドはNext.js、バックエンドはFastAPI、データベースはMySQLで分離しています。FastAPI側はAPI、モデル、スキーマ、サービス、DB接続の責務を分け、SQLAlchemyとAlembicで永続化とマイグレーションを管理します。"
work_features: "JWTユーザー認証 / 資産種別・口座のCRUD API / 月次収支のCRUD API / Alembicマイグレーション / Docker Compose開発環境 / SwaggerによるAPI確認 / Health Check API"
work_learnings: "資産シミュレーションでは計算式だけでなく、入力データの定義と履歴の持ち方が結果の信頼性を左右します。将来機能を見据え、画面より先にドメインモデルとAPIの責務を整理する重要性を学びました。"
work_next_steps: "資産スナップショット、老後条件の設定、積立プラン、シミュレーション計算、ダッシュボードとグラフ、フロントエンド画面、テストコードを追加します。"
work_role: "個人開発 / 要件整理・設計・バックエンド実装"
work_period: "2026年〜開発中"
work_github_url: "https://github.com/masakiShito/wealth-manager"
technologies:
  - "Next.js"
  - "TypeScript"
  - "FastAPI"
  - "Python"
  - "MySQL"
  - "SQLAlchemy"
  - "Alembic"
  - "Docker"
related_posts: []
---

Wealth Managerは、老後資産がどのくらい必要になるかを試算し、現在の資産状況と積立状況で不足がないかを確認するためのWebアプリです。

複数の資産や月次収支を一つのデータモデルで管理し、将来的には退職年齢、生活費、年金、積立条件を使ったシミュレーションへつなげます。

現在はDocker開発環境、JWT認証、資産種別・口座・月次収支のAPI、DBマイグレーションまで実装しています。