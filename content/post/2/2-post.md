---
title: "名前空間用のインスタンス化されないクラスを定義する"
date: 2023-05-09T08:08:48+09:00
draft: false
tags: ["Flutter", "Dart"]
categories: ["Flutter"]
---

# 名前空間用のインスタンス化されないクラスを定義する

swiftやjavaでは、インスタンス化されないクラスを作成するのに、enumやnamespaceを利用します。

これをDartで実現するにはどうすればいいでしょうか？

### 結論
以下のコードの`ErrorMessage._()`という名前付きコンストラクタを定義すると、外部からインスタンス化されないクラスを定義することができる。
```dart
class ErrorMessage {
	const ErrorMessage._(); 

	static const invalidParameter = 'パラメータが間違っています。';
	static const unknown = '予期せぬ不具合が発生しました。';
	static const other = '例外が発生しました。';
}
```


### デフォルトコンストラクタ
`Dart` では、コンストラクタを定義していないクラスはデフォルトで、そのクラスと同じ名前のコンストラクタが作成される。
```Dart
class A {}

// Aというコンストラクタが自動で作成されてインスタンス化
A();
```


しかし、名前付きコンストラクタを定義すると、デフォルトコンストラクタが作成されない。
```dart
class A {
  A.instance();
}

// エラー
A();

// OK
A.instance();
```


### プライベート
`ErrorMessage._();`では、`_` という名前付きコンストラクタを定義している。

`Dart`において、`prefix`に`_`がついたメソッドや変数は`private`となり、外部から参照できない。

そのため、`_`という名前付きコンストラクは外部から参照することができず、インスタンス化はできない。


また、名前付きコンストラクタが定義されているので、通常のコンストラクタも定義されず、外部からインスタンス化することができないクラスが作成できる。


### 課題点1
引数に型を指定することでインスタンスを期待するコードが書けてしまう。

```dart
// こういう引数を書けてしまうことは避けられない
void doSomething(A a) {
    print("Aのインスタンスを期待する処理");
}
```

swiftのenumでは、この場合コンパイラが警告を出してくれるため便利です。

Dartもそうなって欲しいですね。


### 課題点2
プライベート名前付きコンストラクタが定義されたファイル内では、クラス外からそのコンストラクタにアクセスできてしまう。
```dart
class NameSpace {
	NameSpace._();
}

class Hoge {
	// インスタンス化可能！！
	NameSpace._();
}
```

これは、Dartのprivateはクラスレベルではなく、ライブラリ（ファイル）レベルであることが原因です。

クラスは基本的にファイルで分けて定義することが多いので特に問題はないが、
もちろんそうじゃない場合もある（クラス定義ファイルで別のクラスを作成する）ので、気をつける必要がありますね。


### まとめ
Dartにおいて、インスタンス化されない名前空間用のクラスを作成するには、`_`が付いた名前付きコンストラクタを作成します。

それにより、デフォルトコンストラクタが作成されず、外部から参照できないクラスが作成できます。

ただし、引数などに型を指定することで、その型のインスタンスを期待するコードが書けてしまうという課題、同じファイル内からはアクセスができてしまう課題があります。