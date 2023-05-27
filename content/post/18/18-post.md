---
title: "SizedBox, Paddingの代わりに使えるGap widget"
date: 2023-05-24T22:36:32+09:00
draft: false
tags: ["Flutter", "Dart", "Widget"]
categories: ["Flutter"]
---

Flutterでwidget間でスペースを作りたい時に、
- Paddingで囲む
- SizedBoxを使う

の二つのパターンがある。

しかし、`Padding`を使うと、ネストが深くなって見にくくなる。冗長である。
`SizedBox`を使う場合には、`Row`か`Column`の中か知っておく必要があり、`Row`だったら、`SizedBox(width:)`、`Column`だったら、`SizedBox(height:)`のように指定しないといけない。

この冗長さをなくしてくれるのが、`Gap`ウィジェット。

`Column`、`Row`に関わらず、`Gap(20)`などで空きスペースを指定できる。

## 注意点
ただ、パッケージを導入する必要があるので、メンテナンスされなくなったりしたら不安。


## 参考

- https://pub.dev/packages/gap
- [ウィジェットの間にスペースを作りたい時にSizedBoxではなくGapを使うと良い](https://zenn.dev/flutteruniv_dev/articles/702e37e880c9e6)