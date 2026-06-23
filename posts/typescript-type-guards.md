---
title: TypeScriptの型ガードでunknownを安全に扱う
slug: typescript-type-guards
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: beginner
categories:
  - TypeScript
technologies:
  - TypeScript
verified_status: unverified
verified_date: ""
verified_env: Node.js 22 / TypeScript 5.x / macOS
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

外部API、フォーム入力、JSON.parse の戻り値など、実行時まで中身が分からない値を扱う場面はよくあります。

このとき any を使うと一時的には楽ですが、型チェックの恩恵を失いやすくなります。この記事では unknown と型ガードを使って、安全に値を絞り込む方法を紹介します。

## 前提

TypeScript の基本的な型注釈が分かる人を対象にします。

扱う例は、外部からユーザー情報を受け取るケースです。

```ts
const data: unknown = JSON.parse('{"id":1,"name":"Taro"}');
```

## 完成形

最終的には、次のように unknown の値を検証してから安全に使います。

```ts
type User = {
  id: number;
  name: string;
};

function isUser(value: unknown): value is User {
  if (typeof value !== 'object' || value === null) {
    return false;
  }

  const record = value as Record<string, unknown>;

  return typeof record.id === 'number' && typeof record.name === 'string';
}

const data: unknown = JSON.parse('{"id":1,"name":"Taro"}');

if (isUser(data)) {
  console.log(data.name.toUpperCase());
}
```

## 実装手順

まず、期待するデータ構造を型として定義します。

```ts
type User = {
  id: number;
  name: string;
};
```

次に、その型に合っているかを確認する関数を作ります。

```ts
function isUser(value: unknown): value is User {
  if (typeof value !== 'object' || value === null) {
    return false;
  }

  const record = value as Record<string, unknown>;

  return typeof record.id === 'number' && typeof record.name === 'string';
}
```

戻り値の `value is User` が型ガードです。この関数が true を返した場合、TypeScript はその値を User として扱えます。

## よくある詰まりどころ

### object判定だけでは足りない

JavaScript では null も typeof null === 'object' になります。そのため、object 判定と null チェックはセットで書きます。

```ts
if (typeof value !== 'object' || value === null) {
  return false;
}
```

### as User で済ませない

次のように書くと、TypeScriptには伝わりますが、実行時の安全性は上がりません。

```ts
const user = data as User;
```

外部から入る値は、型アサーションではなく実際の条件分岐で確認します。

## まとめ

unknown は、外部から入ってくる値を安全に扱うための型です。

型ガードを組み合わせることで、実行時に値を検証しながら TypeScript の補完も活かせます。まずは API レスポンスや JSON.parse の結果など、境界部分から使うのがおすすめです。
