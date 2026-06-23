---
title: WordPress REST APIでカスタム投稿タイプを取得する基本
slug: wordpress-rest-api-custom-post-type
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: intermediate
categories:
  - WordPress
technologies:
  - WordPress
  - PHP
  - REST API
verified_status: unverified
verified_date: ""
verified_env: WordPress 6.x / PHP 8.x / macOS
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

WordPress で Works や記事をカスタム投稿タイプとして管理している場合、REST API から取得できるようにしておくと、外部アプリや静的サイトとの連携がしやすくなります。

この記事では、カスタム投稿タイプを REST API に公開し、JavaScript から取得する基本を紹介します。

## 前提

WordPress のテーマまたはプラグインで、カスタム投稿タイプを登録できる前提です。

例では work というカスタム投稿タイプを使います。

## 完成形

PHP 側で show_in_rest を有効にします。

```php
add_action('init', function () {
    register_post_type('work', [
        'label' => 'Works',
        'public' => true,
        'show_in_rest' => true,
        'rest_base' => 'works',
        'supports' => ['title', 'editor', 'thumbnail', 'excerpt'],
    ]);
});
```

REST API では次の URL で取得できます。

```text
/wp-json/wp/v2/works
```

## カスタム投稿タイプを登録する

register_post_type で投稿タイプを登録します。

```php
add_action('init', function () {
    register_post_type('work', [
        'label' => 'Works',
        'public' => true,
        'show_in_rest' => true,
        'rest_base' => 'works',
        'supports' => ['title', 'editor'],
    ]);
});
```

重要なのは show_in_rest です。

```php
'show_in_rest' => true,
```

これを有効にすると、REST API から取得できるようになります。

## rest_baseでURLを決める

rest_base を指定すると、REST API のエンドポイント名を決められます。

```php
'rest_base' => 'works',
```

この場合、URL は次のようになります。

```text
/wp-json/wp/v2/works
```

指定しない場合は、投稿タイプ名が使われます。

## JavaScriptから取得する

ブラウザや Node.js から fetch で取得できます。

```ts
type Work = {
  id: number;
  slug: string;
  title: {
    rendered: string;
  };
};

async function fetchWorks(): Promise<Work[]> {
  const response = await fetch('https://example.com/wp-json/wp/v2/works');

  if (!response.ok) {
    throw new Error('Worksの取得に失敗しました');
  }

  return (await response.json()) as Work[];
}
```

## よくある詰まりどころ

### show_in_restを忘れる

カスタム投稿タイプを登録していても、show_in_rest が true でないと REST API には出てきません。

管理画面には表示されるのに API で取れない場合は、まずこの設定を確認します。

### rest_baseと投稿タイプ名を混同する

投稿タイプ名が work でも、rest_base を works にしている場合、API URL は /works です。

### HTMLが含まれる

title.rendered や content.rendered には HTML が含まれることがあります。

表示側では、HTML として表示するのか、テキストとして扱うのかを決めておきます。

## まとめ

カスタム投稿タイプを REST API に公開するには、show_in_rest を有効にします。

rest_base を指定しておくと、API URL を分かりやすくできます。

WordPress のデータを外部から利用したい場合、まずはカスタム投稿タイプの REST API 公開から整えるのがおすすめです。
