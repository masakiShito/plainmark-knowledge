---
title: Zodでフォーム入力をTypeScript安全にバリデーションする
slug: zod-form-validation-typescript
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: intermediate
categories:
  - TypeScript
technologies:
  - TypeScript
  - Zod
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

フォーム入力は、画面上では文字列として扱われることが多いです。

しかし、アプリケーション側では、必須、文字数、メールアドレス形式などのルールで検証する必要があります。

この記事では、Zod を使ってフォーム入力をバリデーションし、TypeScript の型として安全に扱う方法を紹介します。

## 前提

TypeScript の基本と npm パッケージの追加が分かる人を対象にします。

Zod はスキーマ定義とバリデーションを行うライブラリです。

## 完成形

次のような問い合わせフォームの入力を検証します。

```ts
import { z } from 'zod';

const contactSchema = z.object({
  name: z.string().min(1, '名前を入力してください'),
  email: z.string().email('メールアドレスの形式が正しくありません'),
  message: z.string().min(10, 'メッセージは10文字以上で入力してください'),
});

type ContactInput = z.infer<typeof contactSchema>;

const result = contactSchema.safeParse({
  name: 'Taro',
  email: 'taro@example.com',
  message: 'お問い合わせ内容です。',
});

if (!result.success) {
  console.log(result.error.flatten().fieldErrors);
} else {
  const input: ContactInput = result.data;
  console.log(input.email);
}
```

## Zodを追加する

まず、Zod をインストールします。

```bash
npm install zod
```

## スキーマを定義する

フォームで受け取る値のルールをスキーマとして定義します。

```ts
const contactSchema = z.object({
  name: z.string().min(1, '名前を入力してください'),
  email: z.string().email('メールアドレスの形式が正しくありません'),
  message: z.string().min(10, 'メッセージは10文字以上で入力してください'),
});
```

このスキーマは、実行時のバリデーションに使えます。

さらに、TypeScript の型も作れます。

```ts
type ContactInput = z.infer<typeof contactSchema>;
```

## safeParseで検証する

safeParse は、成功・失敗を結果オブジェクトとして返します。

```ts
const result = contactSchema.safeParse(input);

if (!result.success) {
  console.log(result.error);
  return;
}

console.log(result.data);
```

result.success が true の場合、result.data はスキーマを通過した安全な値です。

## FormDataと組み合わせる

フォームから受け取った FormData をオブジェクトに変換して検証します。

```ts
function parseContactForm(formData: FormData) {
  return contactSchema.safeParse({
    name: formData.get('name'),
    email: formData.get('email'),
    message: formData.get('message'),
  });
}
```

FormData.get の戻り値は string、File、null の可能性があります。

Zod の z.string を通すことで、文字列以外はエラーにできます。

## よくある詰まりどころ

### parseとsafeParseの違い

parse は失敗すると例外を投げます。

safeParse は例外を投げず、成功・失敗をオブジェクトで返します。

フォームでは、エラー表示に使いやすい safeParse がおすすめです。

### 型だけでは実行時の値を守れない

TypeScript の型はコンパイル時の仕組みです。

外部から入ってくるフォーム入力は、実行時に検証する必要があります。

## まとめ

Zod を使うと、フォーム入力のバリデーションと TypeScript の型定義をまとめて管理できます。

safeParse を使い、失敗時のエラーを画面に返す形にすると、実装が安定しやすくなります。
