---
title: "baby-handoff — 夫婦の育児をつなぐ引き継ぎWebアプリ"
slug: "baby-handoff"
post_type: "portfolio"
status: "publish"
date: "2026-07-19"
excerpt: "育児ログと引き継ぎメモを夫婦で共有し、次に必要な対応を把握しやすくするWebアプリです。"
work_type: "product"
work_status: "in_progress"
work_summary: "育児ログと引き継ぎメモを夫婦で共有し、今日の状況と次に必要な対応を把握しやすくするWebアプリです。"
work_problem: "育児中は、授乳・食事・睡眠・体温・薬などの情報が細かく積み重なります。口頭やチャットだけの共有では、直前に何をしたか、次に何が必要かが分かりにくく、引き継ぐ側が迷いやすい課題がありました。"
work_solution: "育児ログと引き継ぎメモを同じダッシュボードへ集約し、今日の状態、時系列の記録、注意事項をスマートフォンからすぐ確認できる構成にしました。単なる記録帳ではなく、夫婦の引き継ぎボードとして設計しています。"
work_architecture: "Next.jsのApp RouterとServer Actionsを使い、認証・初期セットアップ・育児ログ・引き継ぎを機能単位で分離しています。Supabase AuthとPostgreSQLを利用し、RLSとサーバー側の権限確認を組み合わせて家族単位のデータを保護します。"
work_features: "メールアドレス認証 / 家族スペースと子どもの登録 / 今日の状態サマリー / 育児ログのタイムライン / 食事・睡眠・体温・薬などの記録 / 引き継ぎメモ / RLSによるデータ保護 / スマートフォン向けUI"
work_learnings: "生活の中で使うアプリでは、機能数よりも入力のしやすさと情報の見つけやすさが重要でした。また、家族データを扱うため、画面だけでなく認証・権限・データ分離を最初から設計する必要があると学びました。"
work_next_steps: "家族招待機能、1日のAI要約、PWA、プッシュ通知、画像アップロード、週次レポートを追加し、実際の夫婦間で継続利用できる状態を目指します。"
work_role: "個人開発 / 企画・UI設計・実装"
work_period: "2026年〜開発中"
work_github_url: "https://github.com/masakiShito/baby-handoff"
technologies:
  - "Next.js"
  - "TypeScript"
  - "Tailwind CSS"
  - "Supabase"
  - "PostgreSQL"
  - "Zod"
  - "Docker"
related_posts: []
---

baby-handoffは、夫婦で育児ログと引き継ぎ情報を共有するためのスマートフォン向けWebアプリです。

食事、睡眠、体温、薬などの記録を時系列で残し、今日の状態と引き継ぎメモをひとつの画面で確認できます。育児記録を蓄積することよりも、交代した人が迷わず次の対応へ移れることを重視しています。

現在は認証、家族スペース、育児ログ、引き継ぎメモ、RLSによるデータ保護まで実装しています。