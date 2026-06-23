---
title: GitHub ActionsでMarkdown記事のfront matterを検証する
slug: github-actions-validate-markdown-frontmatter
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: intermediate
categories:
  - GitHub Actions
technologies:
  - GitHub Actions
  - Node.js
  - Markdown
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

Markdown で記事を管理していると、front matter の書き漏れが起きやすくなります。

たとえば、slug がない、status が想定外、slug とファイル名が一致していない、といった状態です。

この記事では、GitHub Actions で Markdown 記事の front matter を検証する基本的な構成を作ります。

## 前提

記事は posts に置かれている前提です。

```text
posts/
├── typescript-type-guards.md
└── react-useeffect-dependency-array.md
```

## 完成形

Pull Request のたびに、次の項目を検証します。

```text
- title がある
- slug がある
- status が draft / publish のどちらか
- slug とファイル名が一致している
```

## 検証スクリプトを作る

front matter を読み取るために gray-matter を追加します。

```bash
npm install gray-matter
npm install -D typescript tsx @types/node
```

次に、検証スクリプトを作ります。

```ts
import { readdirSync, readFileSync } from 'node:fs';
import { basename, join } from 'node:path';
import matter from 'gray-matter';

const postsDir = 'posts';
const allowedStatus = new Set(['draft', 'publish']);

let hasError = false;

for (const file of readdirSync(postsDir)) {
  if (!file.endsWith('.md')) {
    continue;
  }

  const path = join(postsDir, file);
  const source = readFileSync(path, 'utf8');
  const parsed = matter(source);
  const data = parsed.data;
  const expectedSlug = basename(file, '.md');

  if (!data.title) {
    console.error(`${file}: title がありません`);
    hasError = true;
  }

  if (data.slug !== expectedSlug) {
    console.error(`${file}: slug とファイル名が一致していません`);
    hasError = true;
  }

  if (!allowedStatus.has(data.status)) {
    console.error(`${file}: status が不正です`);
    hasError = true;
  }
}

if (hasError) {
  process.exit(1);
}
```

## npm scriptsを追加する

```json
{
  "scripts": {
    "validate:posts": "tsx scripts/validate-posts.ts"
  }
}
```

ローカルで実行します。

```bash
npm run validate:posts
```

## GitHub Actionsを追加する

.github/workflows/validate-posts.yml を作ります。

```yaml
name: Validate posts

on:
  pull_request:
    paths:
      - posts/**/*.md
      - scripts/validate-posts.ts
      - package.json
      - package-lock.json

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - run: npm ci
      - run: npm run validate:posts
```

## よくある詰まりどころ

### pathsの指定が狭すぎる

paths を指定すると対象ファイルが変わったときだけワークフローが動きます。

検証スクリプトや lock file の変更も対象に入れておく必要があります。

### エラー内容が分かりにくい

CI のログだけで原因が分かるように、ファイル名と項目名を一緒に出力します。

## まとめ

Markdown 記事を GitHub で管理する場合、front matter の検証を CI に入れるとレビューが楽になります。

最初は必須項目と slug の一致だけでも十分です。運用に合わせて、verified_status や tested_path の検証を追加していくと、記事品質を保ちやすくなります。
