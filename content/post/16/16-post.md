---
title: "Dialogと画面の隙間を24pxに設定したいんじゃ！"
date: 2023-05-22T21:56:07+09:00
draft: false
tags: ["Flutter", "Dart"]
categories: ["Flutter"]
---

## はじめに

Flutterのダイアログには、`AlertDialog`と`SimpleDialog`の2種類があります。

この2種類のダイアログは`Dialog`という`widget`をラップして実装されています。

`Dialog widget`を直接使用することもできますが、公式では`AlertDialog`か`SimpleDialog`を使うことが推奨されています。

> Rather than using this widget directly, consider using AlertDialog or SimpleDialog, which implement specific kinds of Material Design dialogs.

`AlertDialog`と`SimpleDialog`には、`contentPadding`、`insetPadding`プロパティというものがあり、それぞれ以下の役割を果たします。

- `contentPadding`
  - ダイアログの`content`周りの`padding`を指定

- `insetPadding`
  - ダイアログの外側の`MediaQueryData.viewInsets`に追加されるpaddingの量を指定
  - 画面の幅とダイアログの間の最小スペースを定義

上記の役割を踏まえると、今回のタイトルにある「Dialogと画面の隙間を24pxに設定したい」を実現させるには、`insetPadding`の値を`24px`にすれば良さそうですね...？

## いざ実装へ

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

{{< figure src="/post/16/dialog-before.png" width="300">}}

このダイアログに対して`insetPadding`を付与して`dialog`と画面の幅を`24px`に設定するようにします。

```dart
AlertDialog(
+ insetPadding: const EdgeInsets.symmetric(horizontal: 24),
  title: const Text('AlertDialog Title'),
  content: const Text('AlertDialog description'),
  ...
```

{{< figure src="/post/16/dialog-medium.png" width="300">}}

...なにも変わらない😇

## なぜダイアログの幅が変わらない？

結論から言うと、`InsetPadding`はダイアログの横幅を大きくすることはできないからです。

以下のように画面幅からダイアログの横幅を引いた値よりも指定した`InsetPadding`の値が大きい時に`InsetPadding`は機能します。
```
ダイアログの横幅 > 画面幅 - InsetPaddingの値(今回は24px) * 2

InsetPadding * 2 > 画面幅 - ダイアログの横幅
```

ダイアログの横幅が変わらなかったのは、指定した`InsetPadding`の値よりも画面幅からダイアログの幅を引いた値の方が大きかったからです。

なので、まずはダイアログの横幅を画面いっぱいにし、そこから`InsetPadding`を指定することで、タイトルにある「Dialogと画面の隙間を24pxに設定する」が実現できそうです。

## ダイアログを画面幅と同じにする

`AlertDialog`の`content`をSizedBoxで囲み、その横幅に`MediaQuery.of(context).size.width`を指定することで、ダイアログの横幅と画面幅を同じにします。（titleをSizedBoxで囲んでもokです）

```dart
AlertDialog(
  insetPadding: const EdgeInsets.symmetric(horizontal: 0),
  title: const Text('AlertDialog Title'),
  content: SizedBox(
    width: MediaQuery.of(context).size.width,
    child: const Text('AlertDialog description'),
  ),
```

`insetPadding`はデフォルトが`EdgeInsets.symmetric(horizontal: 40.0, vertical: 24.0)`となっています。

今回は画面いっぱいにダイアログを広げるところを見せるために、`horizontal: 0`を指定しています。

{{< figure src="/post/16/widthMax-dialog.png" width="300">}}

画面いっぱいにダイアログを広げられましたね。

## ダイアログと画面の隙間を24pxに設定する

ダイアログと画面幅を同じにできたので、あとは`InsetPadding`を24pxに設定するだけです。

```dart
AlertDialog(
  insetPadding: const EdgeInsets.symmetric(horizontal: 24),
  title: const Text('AlertDialog Title'),
  content: SizedBox(
    width: MediaQuery.of(context).size.width,
    child: const Text('AlertDialog description'),
  ),
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
```

{{< figure src="/post/16/24px-dialog.png" width="300">}}

ダイアログと画面の隙間を24pxに設定できました🎉

## 今回詰まった理由
`AlertDialog`には`width`プロパティがなく、明示的に`width`の指定をしていないため、`insetPadding`の値を調整したらダイアログの横幅が変わると勘違いしていました。

そこで、`AlertDialog`がラップしている`Dialog`の実装を見ると、丁寧に`ConstrainedBox`で`minWidth: 280.0`が設定してありました。

```dart
dialogChild = Align(
  alignment: alignment ?? dialogTheme.alignment ?? defaults.alignment!,
  child: ConstrainedBox(
    constraints: const BoxConstraints(minWidth: 280.0), // ここ
    child: Material(
      color: backgroundColor ?? dialogTheme.backgroundColor ?? Theme.of(context).dialogBackgroundColor,
      elevation: elevation ?? dialogTheme.elevation ?? defaults.elevation!,
      shadowColor: shadowColor ?? dialogTheme.shadowColor ?? defaults.shadowColor,
      surfaceTintColor: surfaceTintColor ?? dialogTheme.surfaceTintColor ?? defaults.surfaceTintColor,
      shape: shape ?? dialogTheme.shape ?? defaults.shape!,
      type: MaterialType.card,
      clipBehavior: clipBehavior,
      child: child,
    ),
  ),
);
```

これのおかげで明示的に`width`を指定しなくても`Dialog`に280ピクセルの横幅が付与されていました。😇

## 最後に

昔にも似たようなことで詰まった覚えがあるのですが、すっかり忘れていたことがわかったので、備忘録のためにも今後もアウトプットを続けていきたいと思います💪

## 参考
- [InsetPadding not working correctly in AlertDialog / Dialog](https://github.com/flutter/flutter/issues/61154)
- [ConstrainedBox](https://api.flutter.dev/flutter/widgets/ConstrainedBox-class.html)
- [BoxConstraints](https://api.flutter.dev/flutter/rendering/BoxConstraints-class.html)
- [Dialog](https://api.flutter.dev/flutter/material/Dialog-class.html)