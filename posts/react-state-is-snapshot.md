---
title: "Reactのstateは変数ではなくスナップショットとして考える"
slug: "react-state-is-snapshot"
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
series_order: 1
tested_path: "examples/react-state"
test_command: "node --test"
related_works: []
ci_status: "passing"
ci_checked_at: "2026-06-25T08:47:32Z"
ci_run_url: "https://github.com/masakiShito/plainmark-knowledge/actions/runs/28158265821"
---

# Reactのstateは変数ではなくスナップショットとして考える

## この記事で伝えたいこと

Reactのstateは、普通の変数のように即座に書き換わるものではありません。

あるレンダー時点の値を閉じ込めた「スナップショット」として考えると理解しやすくなります。

## よくある疑問

```jsx
const [count, setCount] = useState(0);

function handleClick() {
  setCount(count + 1);
  console.log(count);
}
```

このコードでボタンを押しても、`console.log(count)` は更新後の値にならないことがあります。

## なぜそうなるのか

`count` は、そのレンダー時点の値です。

`setCount` は次のレンダーを予約しますが、今実行中の関数内にある `count` を直接書き換えるわけではありません。

つまり、イベントハンドラの中で見えている `count` は、現在のレンダー時点のスナップショットです。

## 連続更新したい場合

前回の値をもとに更新したい場合は、関数形式を使います。

```jsx
setCount((prev) => prev + 1);
setCount((prev) => prev + 1);
```

この書き方なら、直前の更新結果をもとに次の値を計算できます。

## まとめ

Reactのstateは「今の変数」ではなく「そのレンダー時点の値」です。

この考え方を持つと、イベントハンドラ内のログや連続更新の挙動を理解しやすくなります。
