---
title: Next.jsのServer Actionsでフォーム送信を実装する基本
slug: nextjs-server-actions-basic-form
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: intermediate
categories:
  - Next.js
technologies:
  - Next.js
  - React
  - TypeScript
verified_status: unverified
verified_date: ""
verified_env: Node.js 22 / Next.js 15.x / TypeScript 5.x / macOS
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

Next.js の Server Actions を使うと、フォーム送信後の処理をサーバー側の関数として書けます。

API Route を別で用意しなくても、フォームから直接サーバー処理を呼び出せるため、シンプルな投稿フォームや問い合わせフォームを作りやすくなります。

## 前提

この記事では、Next.js の App Router を使っている前提で進めます。

React と TypeScript の基本的な知識がある人を対象にします。

## 完成形

次のようなフォームを作ります。

```tsx
export default function ContactPage() {
  async function sendContact(formData: FormData) {
    'use server';

    const name = formData.get('name');
    const message = formData.get('message');

    if (typeof name !== 'string' || name.trim() === '') {
      throw new Error('名前を入力してください');
    }

    if (typeof message !== 'string' || message.trim() === '') {
      throw new Error('メッセージを入力してください');
    }

    console.log({ name, message });
  }

  return (
    <form action={sendContact}>
      <input name='name' />
      <textarea name='message' />
      <button type='submit'>送信</button>
    </form>
  );
}
```

## Server Actionsの基本

Server Actions は、サーバー側で実行される関数です。

関数の中で `use server` を宣言することで、その関数はサーバーで実行されます。

```tsx
async function sendContact(formData: FormData) {
  'use server';

  const name = formData.get('name');
  console.log(name);
}
```

フォーム側では、action に関数を渡します。

```tsx
<form action={sendContact}>
  <input name='name' />
  <button type='submit'>送信</button>
</form>
```

## FormDataから値を取り出す

フォームの入力値は FormData から取得します。

```ts
const name = formData.get('name');
```

FormData.get の戻り値は、文字列とは限りません。

そのため、必ず型を確認します。

```ts
if (typeof name !== 'string') {
  throw new Error('nameが文字列ではありません');
}
```

## バリデーションを追加する

空文字を弾く簡単なバリデーションを追加します。

```ts
if (name.trim() === '') {
  throw new Error('名前を入力してください');
}
```

実際のアプリでは、エラー表示や再入力のしやすさも考える必要があります。

## よくある詰まりどころ

### inputにnameを書き忘れる

FormData は name 属性をもとに値を取得します。

```tsx
<input />
```

このように name がないと、formData.get で値を取得できません。

```tsx
<input name='name' />
```

### クライアント側だけを信用しない

ブラウザ側のバリデーションは便利ですが、サーバー側の検証も必要です。

フォーム送信の最終的な処理はサーバーで行われるため、Server Action 内でも必ず値を確認します。

## まとめ

Server Actions を使うと、フォーム送信処理をサーバー関数としてシンプルに書けます。

まずは FormData から値を取り出し、型チェックとバリデーションを行う形を覚えると実装しやすくなります。
