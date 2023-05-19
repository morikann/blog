---
title: "メソッドチェーンを利用して一時変数を省略する"
date: 2023-05-13T23:01:15+09:00
draft: false
tags: ["Swift", "Refactor"]
categories: ["Swift"]
---

### 一時変数の問題点

ある一連の処理を実現するために、一時変数を作成することがあると思います。

しかし、一時変数を作成することは以下のようなデメリットがあります。
- 命名コストがかかる
- 処理の途中の変数は変な命名になりがちで、可読性を損なう

このような場合、メソッドチェーンを利用することで一時変数を作成する必要がなくなります。

一時変数をなくすことで`無駄な命名を省略でき、コードが美しく`なります。

もちろん、一時変数が有効な場合もあるので、適宜使い分ける必要があります。

### 使用例

一時変数をメソッドチェーンで置き換えた使用例を示します。

コードは以下のことをしています。
1. 引数から受け取った文字列を`,`で分割し、配列に格納
2. 配列内の各文字列の前後の空白を削除し、1文字目を大文字に変換
3. 変換した文字列を最終的に`cityNamesWithoutSpace`に格納
4. `cityNamesWithoutSpace`内に文字が含まれていなければ、空配列を返し、そうでなければそのまま返す

```swift
func getCityNames(from text: String) -> [String] {
  // ","で文字列を分割
  let cityNames = text.components(separatedBy: ",")
  var cityNamesWithoutSpace: [String] = []
  cityNames.forEach { cityName in
      // 前後のスペースを削除し、1文字目を大文字にする
      cityNamesWithoutSpace.append(cityName.trimmingCharacters(in: .whitespaces).capitalized)
  }
  cityNamesWithoutSpace = cityNamesWithoutSpace == [""] ? [] : cityNamesWithoutSpace

  return cityNamesWithoutSpace
}
```

コードを見てわかる通り、無駄な変数が多くて可読性が悪いですね。

このコードをメソッドチェーンを利用することで以下のようにリファクタすることができます。

```swift
func getCityNames(from text: String) -> [String] {
  return text.split(separator: ",")
      .map { $0.trimmingCharacters(in: .whitespaces) }
      .map { $0.prefix(1).uppercased() + $0.dropFirst().lowercased() }
}
```

`map`を利用してメソッドチェーンを実現することで、一時変数が不要になりコードがスッキリしましたね。

また、リファクタに伴い`capitalized`を`prefix(1).uppercased()` + `dropFirst().lowercased()`に修正しました。

### まとめ
一時変数の作成は、命名コストがかかり、可読性を損なうことがある。

そのような場合にメソッドチェーンを利用することで、命名コスト、一時変数の作成を省略でき、可読性を向上させることができる。