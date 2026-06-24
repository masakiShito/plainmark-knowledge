---
title: Node.jsでMarkdownのfront matterを読み取るCLIを作る
slug: nodejs-frontmatter-reader
post_type: post
status: draft
date: 2026-06-23
article_type: tutorial
difficulty: intermediate
categories:
  - Node.js
technologies:
  - Node.js
  - Markdown
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

Markdown で記事を管理していると、title、slug、status などの front matter を一覧化したくなることがあります。

この記事では、Node.js と TypeScript で Markdown ファイルの front matter を読み取り、記事一覧を出力する簡単な CLI を作ります。

## 前提

Markdown ファイルの先頭に YAML front matter がある前提で進めます。

```markdown
---
title: TypeScriptの型ガード
slug: typescript-type-guards
status: draft
---

本文です。
```

## 完成形

次のような CLI を作ります。

```bash
node dist/index.js posts
```

出力例です。

```text
typescript-type-guards | draft | TypeScriptの型ガード
react-useeffect-dependency-array | draft | ReactのuseEffect依存配列
```

## パッケージを追加する

YAML を扱うために gray-matter を使います。

```bash
npm install gray-matter
npm install -D typescript tsx @types/node
```

## Markdownファイルを探す

まず、指定ディレクトリ内の .md ファイルを取得します。

```ts
import { readdirSync, statSync } from 'node:fs';
import { join } from 'node:path';

function findMarkdownFiles(dir: string): string[] {
  const entries = readdirSync(dir);
  const files: string[] = [];

  for (const entry of entries) {
    const path = join(dir, entry);
    const stat = statSync(path);

    if (stat.isDirectory()) {
      files.push(...findMarkdownFiles(path));
      continue;
    }

    if (entry.endsWith('.md')) {
      files.push(path);
    }
  }

  return files;
}
```

## front matterを読み取る

gray-matter を使うと、Markdown の front matter と本文を分けて取得できます。

```ts
import { readFileSync } from 'node:fs';
import matter from 'gray-matter';

function readArticle(path: string) {
  const source = readFileSync(path, 'utf8');
  const parsed = matter(source);

  return {
    title: String(parsed.data.title ?? ''),
    slug: String(parsed.data.slug ?? ''),
    status: String(parsed.data.status ?? ''),
  };
}
```

## CLIとして実行する

コマンドライン引数から対象ディレクトリを受け取ります。

```ts
const targetDir = process.argv[2];

if (!targetDir) {
  console.error('Usage: node dist/index.js <posts-dir>');
  process.exit(1);
}

const files = findMarkdownFiles(targetDir);

for (const file of files) {
  const article = readArticle(file);
  console.log(`${article.slug} | ${article.status} | ${article.title}`);
}
```

## よくある詰まりどころ

### front matterがないファイルをどう扱うか

README やメモ用 Markdown が混ざる場合は、posts ディレクトリだけを対象にするか、front matter がないファイルをスキップする処理を入れます。

### slugとファイル名がズレる

CLI で一覧化するだけでなく、slug とファイル名の一致まで検証すると運用が安定します。

## まとめ

Markdown 記事を GitHub で管理する場合、front matter を読み取る CLI があると一覧確認や検証に使えます。

最初は title、slug、status の表示だけでも十分です。運用が進んだら、review_date や verified_status の確認も追加すると便利です。
