---
title: "Templaterプラグインを使って、daily noteにテンプレートを挿入"
date: 2023-05-14T23:16:13+09:00
draft: false
---

私は[obsidian](https://obsidian.md/)というアプリを使って、日々のTODO、メモの管理を行っています。

このobsidianには`daily note`という、その日のメモページみたいなものがあります。

私は`daily note`に、その日のTODO、学んだこと、考えたことを記録するようにしているのですが、毎回それらのタイトルを記述するのは面倒だと感じました。

また、`daily note`から1年、1ヶ月、1日前のメモを確認できたら復習に便利だと思い、これらを自動化しよう！と考えました。

そこで、[Templater](https://github.com/SilentVoid13/Templater)プラグインというものを見つけて、今回はこのプラグインを利用しました。

## 使ってみる

コミュニティプラグインから`Templater`をインストール、有効化し、optionからテンプレートファイルを格納するフォルダを設定しました。

私は04_Templatesというフォルダを指定しました。

