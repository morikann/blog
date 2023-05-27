---
title: "VSCodeで書いたコードの構造を保ったままobsidianにコピー&ペーストする"
date: 2023-05-19T22:50:09+09:00
draft: false
tags: ["VSCode", "Obsidian"]
categories: ["VSCode"]
---

`VSCode`で書いたコードを`obsidian`にコピペすると、表示が崩れてしまいます。

以下のコードを例として使用します。

```dart
class ErrorDialog extends StatelessWidget {
  const ErrorDialog({super.key, required this.errorDescription});

  final String errorDescription;

  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      title: const Text('エラー'),
      content: Text(errorDescription),
      actions: [
        TextButton(
          onPressed: Navigator.of(context).pop,
          child: const Text('OK'),
        ),
      ],
    );
  }
}
```

これを`obsidian`貼り付けると...

```dart
class ErrorDialog extends StatelessWidget {

const ErrorDialog({super.key, required this.errorDescription});

  

final String errorDescription;

  

@override

Widget build(BuildContext context) {

return AlertDialog(

title: const Text('エラー'),

content: Text(errorDescription),

actions: [

TextButton(

onPressed: Navigator.of(context).pop,

child: const Text('OK'),

),

],

);

}

}
```

こんな感じにコードが崩れちゃいます。

### 解決策

`VSCode`の言語モードをプレーンテキストに変更すればOK！

1. `VSCode`右下にある言語（今回でいう`Dart`）を選択

!["dart"](/post/13/language-dart.png)

2. 言語モード選択画面が出てくるので、プレーンテキストを選択する

!["plain"](/post/13/language-plain.png)

これでコピペ & 貼り付けしてもコードの表示崩れが起きなくなります！