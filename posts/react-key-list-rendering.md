---
title: Reactのリストレンダリングでkeyを正しく使う
slug: react-key-list-rendering
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

React で配列を map して表示するとき、key を指定する必要があります。

key は単なる警告を消すための値ではなく、React が要素の対応関係を判断するための重要な情報です。

## 前提

React の map 表示が分かる人を対象にします。

## 基本形

リストを表示するときは、各要素に一意な key を渡します。

```tsx
type Todo = {
  id: string;
  title: string;
};

export function TodoList({ todos }: { todos: Todo[] }) {
  return (
    <ul>
      {todos.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```

この例では todo.id を key にしています。

## keyの役割

React は再レンダー時に、前回の要素と今回の要素を比較します。

key があると、どの要素が同じものなのかを判断できます。

```text
前回: A, B, C
今回: A, C
```

このとき key が安定していれば、React は B が削除されたと判断できます。

## indexをkeyにしない方がよい理由

配列の index を key にすると、並び替えや削除が起きたときに対応関係が崩れることがあります。

```tsx
{todos.map((todo, index) => (
  <li key={index}>{todo.title}</li>
))}
```

追加も削除も並び替えもない静的なリストなら問題になりにくいですが、更新されるリストでは避けるのが無難です。

## 安定したIDを使う

データに id があるなら、それを使います。

```tsx
<li key={todo.id}>{todo.title}</li>
```

id がない場合は、データを作る時点で id を持たせる設計にすると扱いやすくなります。

## よくある詰まりどころ

### keyを子コンポーネントの中に書く

key は map している場所で指定します。

```tsx
{todos.map((todo) => (
  <TodoItem key={todo.id} todo={todo} />
))}
```

TodoItem の内部で key を指定しても、React がリストの対応関係を判断する情報にはなりません。

### keyに毎回変わる値を使う

Math.random や現在時刻のように毎回変わる値は key に向いていません。

毎回別要素として扱われ、不要な再生成が起きます。

## まとめ

React の key は、リスト内の要素を安定して識別するための値です。

基本はデータが持つ id を使います。index や毎回変わる値を使う前に、そのリストが追加、削除、並び替えされる可能性があるかを確認すると判断しやすくなります。
