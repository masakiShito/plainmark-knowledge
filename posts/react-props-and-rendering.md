---
title: "Reactのpropsは親から渡される読み取り専用の入力値"
slug: "react-props-and-rendering"
post_type: "post"
status: "publish"
date: "2026-06-14"
article_type: "tutorial"
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
series_order: 2
related_works: []
---

# Reactのpropsは親から渡される読み取り専用の入力値

## この記事で伝えたいこと

Reactのpropsは、親コンポーネントから子コンポーネントへ渡される入力値です。

子コンポーネント側でpropsを書き換えるのではなく、必要があれば親に状態を持たせて更新します。

## propsの基本

```jsx
function UserName({ name }) {
  return <p>{name}</p>;
}
```

この `name` がpropsです。

コンポーネントは、propsを受け取ってUIを返します。

## propsは読み取り専用

propsは子コンポーネント内で直接変更するものではありません。

```jsx
function UserName({ name }) {
  name = '別の名前'; // 避ける
  return <p>{name}</p>;
}
```

このように書くと、データの流れが分かりづらくなります。

## 更新したい場合

子から親の状態を更新したい場合は、親から更新関数を渡します。

```jsx
function Parent() {
  const [name, setName] = useState('Taro');
  return <Child name={name} onChangeName={setName} />;
}
```

子は `onChangeName` を呼び出すだけにします。

## まとめ

propsは、コンポーネントに渡される入力値です。

Reactでは、データの流れを親から子へ一方向に保つことで、状態管理を追いやすくします。
