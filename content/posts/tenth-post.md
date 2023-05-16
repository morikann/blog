---
title: "VSCodeでデバッグ"
date: 2023-05-16T22:44:28+09:00
draft: false
---

右クリックで「ログポイントを追加」を選択すると、ログに出力する文字列を書くことができる。
`{}`で囲めば、変数の出力も可能！

`print`での出力と比較して以下の点が個人的に良い。
- printと書いてコードを汚すことがない
- printを消し忘れてコミットすることを防げる
- リビルドしなくてもログに出力する文字列を変更したらすぐに反映される

!["VSCodeDebug"](images/VSCode_Debug.png)


### 参考
https://code.visualstudio.com/docs/editor/debugging

[君はVS Codeのデバッグの知られざる機能について知っているか](https://qiita.com/_ken_/items/c5aa4841be74b06530b4)
