---
title: "Dialogの横幅を画面いっぱいに引き伸ばしたいんじゃ！"
date: 2023-05-22T21:56:07+09:00
draft: false
tags: ["Flutter", "Dart"]
categories: ["Flutter"]
---

### はじめに

Flutterのダイアログには、`AlertDialog`と`SimpleDialog`の2種類があります。

この2種類のダイアログは`Dialog`という`widget`をラップして実装されています。

`Dialog widget`を直接使用することもできますが、公式では`AlertDialog`か`SimpleDialog`を使うことが推奨されています。

> Rather than using this widget directly, consider using AlertDialog or SimpleDialog, which implement specific kinds of Material Design dialogs.

以下では、`AlertDialog`と`SimpleDialog`のことを両widgetと呼ぶこととします。

両widgetには、`contentPadding`プロパティと`insetPadding`プロパティというものがあり、それぞれ以下の役割を果たします。

- `contentPadding`
  - ダイアログの`content`周りの`padding`を指定

- `insetPadding`
  - ダイアログの外側の`MediaQueryData.viewInsets`に追加されるpaddingの量を指定
  - 画面の幅とダイアログの間の最小スペースを定義する

&nbsp;

上記の役割を踏まえると、今回のタイトルにある「Dialogの横幅を画面いっぱいに広げる」には、`insetPadding`の値を`0`にすれば良さそうということがわかります。

そもそも何でこれをやろうかと思ったかというと、案件をやる中で、画面の幅とダイアログの間を24pxに統一したい！という場面があるので、

そのために、この画面の幅とダイアログ間のpaddingを調整する必要性がありました。

### いざ実装へ

まず、シンプルな`AlertDialog`を実装します。

```dart
showDialog(
  context: context,
  builder: (context) {
    return AlertDialog(
      title: const Text('AlertDialog Title'),
      content: const Text('AlertDialog description'),
      actions: <Widget>[
        TextButton(
          onPressed: () => Navigator.pop(context, 'Cancel'),
          child: const Text('Cancel'),
        ),
        TextButton(
          onPressed: () => Navigator.pop(context, 'OK'),
          child: const Text('OK'),
        ),
      ],
    );
  },
)
```
![alt|300x300](images/dialog-before.png)

!["dialog-before"](images/dialog-before.png)

このダイアログに対して`insetPadding`を付与して`dialog`の横幅を画面いっぱいに広げるように指定します。

```dart
AlertDialog(
+ insetPadding: const EdgeInsets.symmetric(horizontal: 0),
  title: const Text('AlertDialog Title'),
  content: const Text('AlertDialog description'),
  ...
```

!["dialog-meduim"](images/dialog-medium.png)


なんも変わらんやないかい！

### なんで横幅だけ画面いっぱいに広げられない？

### dialog周りのコードを見てみる

### Constrainsって？

### 改変したコード & 結果

### まとめ

昔にも似たようなところで詰まった覚えがあるので、すっかり忘れていたことがわかった。

アウトプットしないと忘れてしまうから今後も続けていきたい😇

### 参考
[InsetPadding not working correctly in AlertDialog / Dialog](https://github.com/flutter/flutter/issues/61154)
[ConstrainedBox](https://api.flutter.dev/flutter/widgets/ConstrainedBox-class.html)
[BoxConstraints](https://api.flutter.dev/flutter/rendering/BoxConstraints-class.html)
[Dialog](https://api.flutter.dev/flutter/material/Dialog-class.html)