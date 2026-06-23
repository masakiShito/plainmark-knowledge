---
title: ReactのuseEffect依存配列を安全に書く基本
slug: react-useeffect-dependency-array
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: beginner
categories:
  - React
technologies:
  - React
  - TypeScript
verified_status: unverified
verified_date: ""
verified_env: Node.js 22 / React 19.x / TypeScript 5.x / macOS
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

React の useEffect は便利ですが、依存配列の書き方を間違えると、再レンダーのたびに処理が走ったり、逆に古い値を参照したりします。

この記事では、useEffect の依存配列を安全に書くための基本を整理します。

## 前提

React の関数コンポーネントと useState の基本が分かる人を対象にします。

## useEffectの基本

useEffect は、レンダー後に副作用を実行するための Hook です。

```tsx
import { useEffect, useState } from 'react';

export function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(count);
  }, [count]);

  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

この例では count が変わるたびに effect が実行されます。

## 依存配列に入れるもの

useEffect の中で参照している props、state、関数、変数は基本的に依存配列へ入れます。

```tsx
useEffect(() => {
  document.title = `count: ${count}`;
}, [count]);
```

count を参照しているため、依存配列にも count を書きます。

## 空配列は初回だけ

依存配列を空にすると、基本的にはマウント時だけ実行されます。

```tsx
useEffect(() => {
  console.log('mounted');
}, []);
```

ただし、effect の中で props や state を参照しているのに空配列にすると、古い値を参照する原因になります。

## よくある失敗

### 依存配列から値を外す

```tsx
useEffect(() => {
  console.log(userId);
}, []);
```

このコードでは userId が変わっても effect は再実行されません。userId を使っているなら、依存配列に入れます。

```tsx
useEffect(() => {
  console.log(userId);
}, [userId]);
```

### effectの責務が大きすぎる

effect の中に複数の目的を詰め込むと、依存配列が複雑になります。

データ取得、タイトル変更、イベント購読など、目的が違う処理は effect を分けると読みやすくなります。

```tsx
useEffect(() => {
  document.title = `count: ${count}`;
}, [count]);

useEffect(() => {
  console.log('user changed', userId);
}, [userId]);
```

## ESLintに任せる

React の Hooks ルールを守るには、eslint-plugin-react-hooks を使うのがおすすめです。

依存配列の不足を自分で見つけるのは難しいため、警告が出たらまずは理由を確認します。

## まとめ

useEffect の依存配列は、effect の中で参照している値を正直に書くのが基本です。

無理に依存を外すより、処理を effect の中に閉じ込める、コンポーネントを分ける、イベントハンドラに移すなど、設計側で整理すると安定します。
