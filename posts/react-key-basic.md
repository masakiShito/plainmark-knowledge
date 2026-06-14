---
title: "Reactのkeyは配列要素を識別するための印"
slug: "react-key-basic"
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
verified_date: ""
verified_env: ""
review_date: "2026-09-14"
series_name: "React基礎理解"
series_order: 3
related_works: []
---

# Reactのkeyは配列要素を識別するための印

## この記事で伝えたいこと

Reactの`key`は、配列で表示する要素をReactが識別するための印です。

見た目のためではなく、更新時にどの要素が同じものかを判断するために使われます。

## 基本例

```jsx
const users = [
  { id: 1, name: 'Taro' },
  { id: 2, name: 'Hanako' },
];

return users.map((user) => (
  <li key={user.id}>{user.name}</li>
));
```

`key`には、できるだけ安定した一意の値を使います。

## indexをkeyにする問題

```jsx
users.map((user, index) => (
  <li key={index}>{user.name}</li>
));
```

並び替えや削除がない単純なリストなら問題になりにくいですが、要素の順番が変わる場合は注意が必要です。

indexをkeyにすると、Reactが「同じ位置にあるから同じ要素」と判断してしまうことがあります。

## keyに向いている値

- データベースのID
- APIから返るID
- ファイル名やslug
- 一意で変わりにくい値

## まとめ

Reactのkeyは、配列要素の同一性をReactに伝えるためのものです。

迷ったら、表示順ではなくデータそのものに紐づくIDを使うのが安全です。
