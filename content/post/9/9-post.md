---
title: "Simulatorで簡単に画面録画をする方法"
date: 2023-05-15T21:46:55+09:00
draft: false
tags: ["Swift", "XCode", "ショートカット"]
categories: ["XCode"]
---

### 結論
Simulatorを選択状態で`command + R`で録画。

もしくは、Simulator上で`option`キーを押すことで、スクショボタンが録画ボタンに変更されるので、それをクリックすればOK。

| before | after |
| --- | --- |
| !["before-simulator"](/post/9/before-simulator.png) | !["after-simulator"](/post/9/after-simulator.png) |


### 感想

これまでSimulatorの画面録画は以下のコマンドで行なっていました。

```sh
xcrun simctl io booted recordVideo test.mp4
```

しかし、このコマンドは覚えにくく、毎回メモを見に行く → コピー → ターミナルに貼り付けと少し面倒でした。

なので、今後は今回見つけたやり方で録画をしていこうと思います💪



