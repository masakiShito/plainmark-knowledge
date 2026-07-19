---
title: "SpecForge — 設計書の品質と再現性を高めるドキュメント基盤"
slug: "specforge"
post_type: "portfolio"
status: "publish"
date: "2026-07-19"
excerpt: "設計書を構造化データとして扱い、必須項目や参照整合性を検査するためのプラットフォームです。"
work_type: "product"
work_status: "in_progress"
work_summary: "設計書を構造化データとして扱い、必須項目・参照整合性・命名の一貫性を検査できるドキュメント基盤です。"
work_problem: "設計書の品質は執筆者の経験や記述スタイルに依存しやすく、体裁は整っていても必要な情報が不足していたり、別の文書から再利用しにくかったりします。Markdownの自由度だけでは、設計としての完全性を安定して担保できません。"
work_solution: "設計書を自由文ではなく構造化された内部モデルとして保持し、スキーマとLintルールで必須項目不足、参照切れ、命名揺れを検出します。Markdown、HTML、PDFは内部モデルから生成する出力形式として扱います。"
work_architecture: "Next.jsのWebアプリ、FastAPI、PostgreSQLをappsへ分離し、document-schema、editor-engine、lint-rules、共通UIをpackagesとして管理するモノレポ構成です。ドメインモデルと品質ルールを画面や出力形式から独立させる方針にしています。"
work_features: "構造化フォームによる設計書入力 / セクション・フィールド単位の検証 / 参照整合性チェック / 品質警告 / Markdown・HTML・PDF出力 / API保存と検証 / 将来的なAI補助提案"
work_learnings: "ドキュメント品質を高めるには、文章の書き方を統一するだけでなく、必要な情報を型と制約として表現する必要があります。実装前にプロダクト思想とアーキテクチャ原則を文書化することで、責務の混在を防ぎやすくなりました。"
work_next_steps: "設計書入力UI、内部ドキュメントモデル、Lintルール、保存APIを実装し、各出力形式とAI補助を段階的に追加します。"
work_role: "個人開発 / プロダクト設計・アーキテクチャ設計"
work_period: "2026年〜設計・基盤開発中"
work_github_url: "https://github.com/masakiShito/specforge"
work_demo_url: ""
technologies:
  - "Next.js"
  - "TypeScript"
  - "FastAPI"
  - "Python"
  - "PostgreSQL"
  - "pnpm"
  - "Docker"
related_posts: []
---

SpecForgeは、設計書を単なるMarkdownや文章ファイルではなく、検証可能な構造化データとして扱うためのプラットフォームです。

必須項目の不足、文書間の参照切れ、命名の揺れなどを自動検出し、誰が作成しても一定品質を保ちやすい設計書運用を目指しています。

現在はプロダクトビジョン、品質原則、リポジトリ構成、アーキテクチャ原則を定義し、Next.js、FastAPI、PostgreSQLを使った開発基盤を整備しています。