---
title: "Hugoで記事内の画像サイズを変更する"
date: 2023-05-25T23:56:26+09:00
draft: false
tags: ["Hugo"]
categories: ["Hugo"]
---

マークダウンでは以下の記法を用いて画像を表示します。
```
![画像名](画像パス)
```

Hugoの記事においても、上記の書き方で画像を表示することはできます。

が、画像サイズの調整ができません。

## 画像サイズを変更する

Hugoには、shortcode方式というものがあるそうで、それを使うことで画像サイズの指定ができます。


{{&lt; figure src="/images/image.png" title="Screenshot" class="center" width="320" height="640" &gt;}}


他にも属性があったり、shortcodeを利用してyoutubeなども埋め込めるそうです。

詳細は[公式ページ](https://gohugo.io/content-management/shortcodes/)に記載されています。

## 参考
- [Hugoで記事内に画像を貼り付ける方法](https://qiita.com/atuyosi/items/4100bd502e373c088c74)

