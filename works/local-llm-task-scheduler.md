---
title: "Local LLM Task Scheduler — 再現性を重視した予定生成システム"
slug: "local-llm-task-scheduler"
post_type: "portfolio"
status: "publish"
date: "2026-07-19"
excerpt: "決定論的な予定生成ロジックとLocal LLMの説明機能を分離したタスク管理システムです。"
work_type: "product"
work_status: "in_progress"
work_summary: "決定論的な予定生成ロジックとLocal LLMの説明機能を分離し、その日の空き時間へ実行可能なタスク案を割り当てるシステムです。"
work_problem: "一般的なTodoアプリでは、期限や優先度は管理できても、実際の空き時間へどう配置するかは利用者自身が考える必要があります。一方で、LLMへ計画を丸投げすると同じ入力でも結果が変わり、理由や失敗条件を検証しにくい課題があります。"
work_solution: "空き時間の算出とタスク割り当てはルールベースの決定論的ロジックで実行し、LLMは計画理由や入りきらなかったタスクの説明だけを担当します。結果は提案として保存し、利用者が最終判断できる設計にしました。"
work_architecture: "Next.js、FastAPI、PostgreSQL、Ollamaを分離し、スケジューリングロジックとLLM処理の責務を分けています。要件定義、基本設計、詳細設計、API、バリデーション、エラー、永続化、テスト設計を文書化し、実装前に整合性を確認できる構成です。"
work_features: "Todo・計画タスク管理 / 固定予定管理 / 空き時間算出 / 優先度・期限・工数による割り当て / 休憩とバッファの挿入 / overflowとwarningの出力 / LLMによる説明生成 / 計画結果の保存"
work_learnings: "AIを使うこと自体ではなく、どの判断をロジックへ残し、どの説明をLLMへ任せるかを明確にすることが重要でした。再現性、テスト可能性、失敗時の説明まで含めてAI機能を設計する視点を整理できました。"
work_next_steps: "設計書に基づくMVP実装、計画の再生成とロック、週単位の最適化、Googleカレンダー連携、実績データを使った見積もり改善を進めます。"
work_role: "個人開発 / 要件定義・基本設計・詳細設計"
work_period: "2026年〜設計完了・実装準備中"
work_github_url: "https://github.com/masakiShito/local-llm-task-scheduler"
work_demo_url: ""
technologies:
  - "Next.js"
  - "FastAPI"
  - "PostgreSQL"
  - "Ollama"
  - "Docker"
  - "LLM"
related_posts: []
---

Local LLM Task Schedulerは、Todoと工数・期限・優先度を持つ計画タスクを統合し、その日の空き時間へ実行可能な時間割を割り当てるタスク管理システムです。

スケジューリングをLLMへ丸投げせず、同じ入力から同じ結果を返す決定論的なロジックで計画を生成します。LLMは、生成した計画の説明や入りきらなかった理由を自然な文章へ変換する補助役として利用します。

現在は要件定義、基本設計、詳細設計まで完了しており、設計書に沿ったMVP実装を次の段階としています。