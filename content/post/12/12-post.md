---
title: "git tagって？"
date: 2023-05-18T21:03:43+09:00
draft: false
tags: ["Git", "Github"]
categories: ["Git"]
---

業務において`git`の`tag`を使う場面があったのですが、あまりどんなものか分からず使っていました。

そのため、今回は`tag`について備忘録として記事に残すことにしました。

## git tag とは？

`git tag`とは、コミット履歴上の重要なポイント(コミット)に印をつける機能。

## いつ使うの？

`v1.0`などのリリースポイントで`tag`を使うことがよくあるそうです。

各リリースポイントで`tag`をつけておくことによって、あるバージョンで起こったバグを再現したい！といった際に、
そのバージョンの`tag`にチェックアウトするだけで簡単にバグの検証をすることができます。

また、どのバージョンで起こったバグか分からない！といったときでも、`tag`を利用して各バージョンの動作検証をすることで、どのバージョンでバグが発生したのかを見つけることができます。

その他にも以下のメリットがあるそうです。
- Github上で、タグ付けした時点の圧縮ファイルをダウンロードできる
- Github上で、タグがあるとリリースノートを作成できる
  - 前回のタグと比較して差分からリリースノートを自動生成できるらしい（詳しくは[こちら](https://docs.github.com/ja/repositories/releasing-projects-on-github/automatically-generated-release-notes)）
- どのコミット時点で本番リリースしたのか参照しやすくなる

## コマンド一覧

### タグの作成

タグには軽量タグと注釈付きタグがある。

- 軽量タグ
  - 変更のないブランチのようなもので、特定のコミットに対する単なるポインタでしかない
  - タグ選択状態でコミットしても、タグが指すコミットの位置は変わらない（注釈付きタグも同様）
  - `$ git tag <タグ名>`でタグを作成

- 注釈付きタグ
  - タグ付けした人の情報、日時、コメントも格納される。
  - `$ git tag -a <タグ名> -m <コメント>`でタグを作成


タグについての詳細を後から確認するためにも、基本的には注釈付きタグを使うのが良さそうですね。

注意点として、コミットを指定せずにタグを作成した場合は、現在のブランチの最新のコミットに対してタグが付与されます。

#### 後からタグを付与する

あるコミットにタグを付与するのを忘れていた場合は、そのコミットハッシュを指定してタグを作成すれば大丈夫です。

`$ git tag -a <タグ名> -m <コメント> <コミットハッシュ>(例：9fceb02)`

### タグの表示

以下のコマンドでタグの一覧を表示する。

`$ git tag`

タグのデータとそれに関連づけられたコミットを見るには、`show`コマンドを使う。

`$ git show <タグ>`

軽量タグの場合は、タグを付与したコミットに関する情報のみ表示される。

注釈付きタグの場合は、タグの作者、作成日時、作成時のコメント + コミット情報が表示される。

以下に注釈付きタグを`show`した際の結果を示す。（`s4`は適当につけたタグ名なので気になさらず）

```
$ git show s4
tag s4
Tagger: morikann <mrknt0088@gmail.com>
Date:   Mon May 22 21:21:24 2023 +0900

タグのコメント

~ 以下にコミット情報が表示 ~ 
```

### タグをリモートにプッシュ

デフォルトでは`git push`コマンドは、タグをリモートに送らないので、タグをリモートにpushすることを明示する必要がある。

以下のコマンドを実行することでタグをリモートにpushできる。

`$ git push <リモート名> <タグ名>`

例：`$ git push origin v1.0`

多くのタグを一度にプッシュしたい場合は、`git push`コマンドのオプション`--tags`を使用する。
これは、ローカルのタグの中でまだリモートに存在しないものをすべて送る。

`$ git push origin --tags`

### リモートのタグをローカルに反映

誰かが作ったリモートのタグをローカルに反映するには以下のコマンドを使う。

`$ git fetch --tags`

## まとめ

`タグについて完全に理解した`

次は`Github`上からタグを利用してリリースノートの自動生成とかやってみたい！

## 参考
- [Git の基本 - タグ](https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E5%9F%BA%E6%9C%AC-%E3%82%BF%E3%82%B0)
- [【Git】git tag について全然知らなかったので色々と調べてみた](https://tec.tecotec.co.jp/entry/2022/12/14/000000)
- [git tagの使い方まとめ](https://qiita.com/growsic/items/ed67e03fda5ab7ef9d08)