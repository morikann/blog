---
title: "ディレクトリ構成をターミナルで出力"
date: 2023-05-23T09:36:16+09:00
draft: false
tags: ["ターミナル", "マークダウン"]
categories: ["ターミナル"]
---

1. `Homebrew`から`tree`をインストール

   - `$ brew install tree`

2. 対象のフォルダに移動してターミナルで`tree`と打つ

   - `$ tree`

!["tree"](images/tree.png)

### マークダウンで表示するには？

ブロックコードの中に書くことでマークダウンでも正常に表示されます。

```
.
├── component
│   └── error_dialog.dart
├── launch_page.dart
└── weather
    ├── component
    │   └── weather_forecast.dart
    ├── weather_page.dart
    ├── weather_page_ui_state.dart
    └── weather_page_ui_state.freezed.dart
```