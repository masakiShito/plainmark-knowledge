---
title: TypeScriptのanyとunknownの違いを実装目線で理解する
slug: typescript-any-vs-unknown
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

TypeScript では、型が分からない値を扱うときに any と unknown が使えます。

どちらも何が入るか分からない値に見えますが、実装上の安全性は大きく違います。

## anyとは

any は TypeScript の型チェックをほぼ無効にする型です。

```ts
let value: any = 'hello';

value.toUpperCase();
value.notExists();
```

存在しないメソッドを呼び出しても、コンパイル時には止まりません。

実行時に壊れる可能性があっても、TypeScript は検出できなくなります。

## unknownとは

unknown は、何が入るか分からない値を表す型です。

ただし、使う前に型を確認する必要があります。

```ts
let value: unknown = 'hello';

if (typeof value === 'string') {
  console.log(value.toUpperCase());
}
```

このように、型を絞り込んだあとであれば安全に使えます。

## 使い分け

基本的には、外部から入ってくる値には unknown を使います。

```ts
function parseJson(source: string): unknown {
  return JSON.parse(source);
}
```

JSON の中身は実行時まで分からないため、戻り値を unknown にしておくと、使う側で検証する流れを作れます。

## anyを使ってよい場面

any を完全に禁止すると、古いライブラリや段階的な移行で困ることがあります。

ただし、使う場合は範囲を狭くします。

```ts
const legacyValue = legacyFunction() as any;
```

ファイル全体やアプリ全体に any を広げるのではなく、境界部分だけに閉じ込めます。

## よくある詰まりどころ

### anyは便利だが型安全ではない

any はエラーを消してくれますが、問題を解決しているわけではありません。

一時的に通すために使った場合は、後で unknown や具体的な型に置き換えるのがおすすめです。

### unknownは面倒に見える

unknown は毎回チェックが必要なので、最初は面倒に感じます。

しかし、境界で一度検証すれば、アプリ内部では安全な型として扱えます。

```ts
if (!isUser(value)) {
  throw new Error('invalid user');
}

// ここから先は User として扱える
```

## まとめ

any は型チェックを弱めるための逃げ道です。

unknown は、分からない値を安全に扱うための型です。

外部入力、APIレスポンス、JSON.parse の戻り値には unknown を使い、型ガードやバリデーションで絞り込む形にすると、実装が安定します。
