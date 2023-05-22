---
title: "hugoで空行を挿入する方法"
date: 2023-05-21T19:12:09+09:00
draft: false
tags: ["Hugo", "マークダウン"]
categories: ["Hugo"]
---

「マークダウン 空行」と調べると、大抵`<br />`を使う方法が出てくる。

しかし、この`hugo`で作っているブログの記事はマークダウンで書いているのにも関わらず、`<br />`で期待した空行ができない。

| マークダウン | 結果 |
| --- | --- |
| !["markdwon-before"](images/space_before.png) | !["ブラウザ-before"](images/space_browzer_before.png) |

### `&nbsp;`で空行を挿入できた

`<br />`の代わりに`&nbsp;`を書くことで、空行を挿入することができました！

| マークダウン | 結果 |
| --- | --- |
| !["markdown-after"](images/space_markdwon_after.png) | !["space-browzer"](images/space_browzer_after.png) |

### 参考
https://open-groove.net/other-tools/markdown-multi-blanklines-hugo/