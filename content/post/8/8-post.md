---
title: "Templaterプラグインを使って、daily noteにテンプレートを挿入"
date: 2023-05-14T23:16:13+09:00
draft: false
tags: ["Obsidian", "自動化"]
categories: ["Obsidian"]
---

私は[obsidian](https://obsidian.md/)というアプリを使って、日々のTODO、メモの管理を行っています。

このobsidianには`daily note`という、その日のメモページみたいなものがあり、私は`daily note`に、その日のTODO、学んだこと、考えたことを記録するようにしています。

しかし、毎日のメモに対してそれらのタイトルを記述するのは面倒だと感じました。

また、`daily note`から1年、1ヶ月、1日前のメモを確認できたら復習に便利だと思い、これらを自動化しよう！と考えました。

そこで、[Templater](https://github.com/SilentVoid13/Templater)プラグインというものを見つけて、このプラグインを利用しました。

## 手順

以下に手順を示します。

1. コミュニティプラグインから`Templater`をインストール、有効化

2. optionからテンプレートファイルを格納するフォルダを設定


!["templates"](/post/8/templates.png)

3. `04_Templates`配下に、テンプレートファイルを作成


!["Daily_templates"](/post/8/Daily_Templates.png)

4. テンプレートを作成するためのコマンドを記述

コマンドについては、[公式ドキュメント](https://silentvoid13.github.io/Templater/internal-functions/overview.html)を参考に記述しました。

コマンドに記載したものは以下の通りです。
- 1年前、1ヶ月前、1日前、1日後の`daily note`
- その日に意識することを書いたカードへのリンク
- TODO、学んだこと、考えたことのタイトル

```
ーーー
Last year: [[<% tp.date.now("YYYY-MM-DD", "P-1Y", tp.file.title, "YYYY-MM-DD") %>]]
Last month: [[<% tp.date.now("YYYY-MM-DD", "P-1M", tp.file.title, "YYYY-MM-DD") %>]]

[[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>]]  |  [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>]]
ーーー

[[意識すること]]

# TODO
- [ ] 

# 学んだこと
- 

# 考えたこと
- 
```

5. `daily note`に先ほど作成したテンプレートを挿入するように設定

私は`daily note`が`02_Daily`フォルダ以下にあるため、そのフォルダに対して先ほど作成した`Daily_Template.md`を適応するように設定しています。

!["setting_template"](/post/8/settings_template.png)

6. 完成！

`daily note`を作成すると、以下のようにテンプレートが挿入されています🎉
!["my_template"](/post/8/my_templates2.png)


## まとめ
今回は`Templater`というプラグインを使って`daily note`にテンプレートを挿入するよう設定を行いました。

これで毎日のメモの基盤ができ、復習も容易になり、良きメモ生活が送れそうです😎