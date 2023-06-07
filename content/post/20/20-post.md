---
title: "flutterプロジェクト作成時にemptyオプションを使用する"
date: 2023-06-07T23:59:23+09:00
draft: false
tags: ["Flutter"]
categories: ["Flutter"]
---

emptyオプションを使用してflutterプロジェクトを作成することができます。

`flutter create --empty [プロジェクト名]`

このオプションを使用することで通常の作成と比べて以下の点が異なります。
- `main.dart`や`pubspec.yaml`から余分なコメントが排除される
	- `flutter create`でプロジェクトを作成すると余分なコメントが多くて毎回消すの大変
- `Hello World`のみが表示されるシンプルなプロジェクトが生成される
- `test`ディレクトリは作成されない
- `README.md`の内容がシンプル

このオプションのドキュメントはなさそうなので、この[issue](https://github.com/flutter/flutter/issues/113853)と[プルリク](https://github.com/flutter/flutter/pull/113873)を読むしかなさそうです🤔

作成されるプロジェクトの外観は以下です。

{{< figure src="/post/20/empty.png" width="300">}}

そして、`README.md`は以下です。

```md
# [プロジェクト名]

A new Flutter project.
```

## まとめ
--emptyオプションを利用することで毎回消すのがめんどくさいコメントが排除されたプロジェクトを生成してくれて便利ですね！

ただ、web、linux、windows、macosディレクトリなどは適宜自分で削除する必要があります💪
