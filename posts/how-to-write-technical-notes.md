---
title: "あとで使える技術メモの書き方"
slug: "how-to-write-technical-notes"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tech_note"
difficulty: "beginner"
categories:
  - "Writing"
technologies:
  - "Markdown"
  - "Knowledge Management"
verified_status: "unverified"
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: "ナレッジ運用入門"
series_order: 1
related_works: []
---

# あとで使える技術メモの書き方

## この記事で伝えたいこと

技術メモは、未来の自分が迷わず再利用できる形で書くと価値が上がります。

単に「何をしたか」だけでなく、「なぜそうしたか」「どこで迷ったか」まで残すことが大切です。

## 悪いメモの例

```text
Reactでstateを更新した。
useStateを使った。
```

これだけだと、あとから読んでも何に困っていたのか分かりません。

## 良いメモの構成

```text
1. 何に困ったか
2. 結論
3. 試したこと
4. うまくいかなかったこと
5. 最終的な実装
6. 次に見るべきリンクや関連知識
```

## 先に結論を書く

技術メモは、最初に結論を書くと読み返しやすくなります。

```text
結論: useStateの更新直後に値を読んでも、同じレンダー内では古い値のまま見える。
```

このように書いておくと、検索で見つけたときにすぐ思い出せます。

## 判断理由を書く

実務では、正解そのものよりも判断理由が重要になることがあります。

- なぜこのライブラリを選んだか
- なぜこの設計を避けたか
- なぜこの実装に落ち着いたか

ここを書いておくと、同じ判断を再利用できます。

## まとめ

技術メモは「記録」ではなく「再利用する知識」です。

未来の自分が同じことで迷わないように、背景・判断・失敗も含めて残すのが良いです。
