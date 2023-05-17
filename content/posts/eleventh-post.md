---
title: "@visibleForTestingとは？"
date: 2023-05-17T21:55:15+09:00
draft: false
tags: ["Flutter", "Dart", "Test"]
categories: ["Flutter"]
---

### はじめに

あるメソッドや`Widget`をテストしたい時は、それらが`test`フォルダから参照できるようにするために`public`にする必要があります。

しかし、`unitテスト`のためにメソッドを`private`から`public`に変更して外部から参照できるようにするのは、安全性が低くなってしまい微妙です。

また、`Widget`をコンポーネントとして切り出すときは、基本的に`private`にしますが、これもテストのために`public`にするのはあまり良い手段だとは言えません。

このような悩みを解決するのが`@visibleForTesting`です。

### @visibleForTestingって？

[公式ページ](https://api.flutter.dev/flutter/meta/visibleForTesting-constant.html)では以下のように記載されています。

> Used to annotate a declaration that was made public, so that it is more visible than otherwise necessary, to make code testable.

> Tools, such as the analyzer, can provide feedback if
> the annotation is associated with a declaration not in the lib folder of a package, or a private declaration, or a declaration in an unnamed static extension, or
the declaration is referenced outside of its defining library or a library which is in the test folder of the defining package.

簡単に要約すると以下の通りです。

コードをtestableにするアノテーションやで💪

@visibleForTestingを付ければ、定義されたもの(関数やクラスなど)が定義ファイル、もしくは`test`フォルダ外から参照された場合、`analyzer`がフィードバック(警告)出すぜ！って感じです。

つまり、このアノテーションをつけることで、テストのために`public`にしたメソッドや`Widget`が他ファイルから参照されるのを防ぐことができます。

これで`test`のために`private`から`public`に変更したコードが他ファイルから使われることを防げそうですね！

### 使用例
`toMap`メソッドをテストするために`public`にした例を示します。

```
@visibleForTesting
Map<String, dynamic> toMap(String json) {
  return jsonDecode(json) as Map<String, dynamic>;
}
```

上記のコードでは、`@visibleForTesting`アノテーションを付けているので他ファイルから参照すると以下のような警告が出ます。

!["visibleForTesting_warning"](images/visibleForTesting_warning.png)


### 警告は無視できるじゃないか

ここで一点問題があります。

そうです、警告は無視できちゃうんです。できれば`warning`ではなく`error`を出すようにしてビルドできないようにしたいですね。

そんな時は、`Dart analysis`の機能を活用します。

`analysis_options.yaml`に以下を記述するだけです。

```yaml
analyzer:
  errors:
    invalid_use_of_visible_for_testing_member: error
```

これで警告がコンパイルエラーに変わりました🎉

!["visibleForTesting_error"](images/visibleForTesting_error.png)

### まとめ
`@visibleForTesting`アノテーションを使うことで不必要なコードの参照を検出できて便利。

また、`Dart analysis`の機能を活用することで、警告をコンパイルエラー変更することができて素晴らしい💪

### 参考
[meta library](https://api.flutter.dev/flutter/meta/meta-library.html)

[visibleForTesting](https://api.flutter.dev/flutter/meta/visibleForTesting-constant.html)

[Flutterでテストコードだけが外部参照できるWidgetを組みたかった](https://scrapbox.io/kurogoma4d-lab/Flutter%E3%81%A7%E3%83%86%E3%82%B9%E3%83%88%E3%82%B3%E3%83%BC%E3%83%89%E3%81%A0%E3%81%91%E3%81%8C%E5%A4%96%E9%83%A8%E5%8F%82%E7%85%A7%E3%81%A7%E3%81%8D%E3%82%8BWidget%E3%82%92%E7%B5%84%E3%81%BF%E3%81%9F%E3%81%8B%E3%81%A3%E3%81%9F)