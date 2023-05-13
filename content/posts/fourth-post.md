---
title: "よく使っているショートカット一覧"
date: 2023-05-11T00:47:57+09:00
draft: false
tags: ["ショートカット"]
categories: ["ショートカット"]
---

備忘録として思いつく限りの使っているショートカットをまとめる。

### ブラウザ
- `command + L`：アドレスバーを選択
- `/`：検索窓にカーソルを移動
- `command + ←`：google chromeの検索で前のページに戻る
- `command + T`：タブ作成
- `command + W`：タブ削除
- `command + R`：ブラウザ更新

### VSCode
- `control + H`：前の文字を一文字削除
  - 小指でDeleteキーを押すのは辛いので便利
- `control + D`：後ろの文字を一文字削除
- `control + K`：カーソルから後ろの文字を削除
- `control + A`：行頭に移動
	- `control + A` -> `control + K`：その行を全削除
- `control + E`：行の最後に移動
- `shift + カーソル`：範囲選択
    - `shift + option + カーソル`：単語単位で範囲選択
- `option + ← or →` : 単語単位での移動
- `command + カーソル`：端に移動
    - control + Aよりこっちの方が使いやすい
- `command + d`：単語選択
- `option + shift + ↓`：複製
- `command + enter`：1番後ろまで移動しなくても改行できる
- `option + ↑ or ↓`：行の入れ替え
- `command + F`: ファイル内検索
- `command + shift + F`: 横断検索
- `F2`：名前の一括変換
- `F12`：定義元を参照
- `F12 + option`：定義元ファイルに飛ばず、ピークで定義を参照
- `command + .`：クイックフィックス（エラーやlint警告などの修正案を出してくれる）
- `command + P`：ファイル検索
- `command + w`：タブ(ファイル)を閉じる
- `command + shift + P`: コマンドパレットを表示
- `command shift + O`：表示しているファイル内のシンボル（関数,クラス,メソッド,コンストラクタなど）の一覧を表示
  - 続いて「`:`」をタイプすると、シンボルがクラスやメソッドなどのカテゴリごとにソートされる
- `command + T`：シンボル名で検索
- `ctrl + -`：元にいた場所に戻る
- `command + B`：サイドバーの表示、非表示を切り替える

### Obsidian
- `command + K`：外部リンクの挿入
- `option + Enter`：バックリンクに飛ぶ
- `command + P`：コマンドパレットを開く（ホットキーの確認などができる）
- `command + ,`：設定を開く（VSCodeなども同様）
- `command + enter`：todo のトグル
- `control + T` create or edit task

### XCode
- `command + shift + N` : 新しいフォルダを作成できる
- `command + A` (ファイルの内容を全て選択) → `control + i` でリフォーマット
- `command + [ or ]`：選択した行のコードを前後に移動させる（VSCodeでも可）
- `command + option + ←`：関数、クラスなどが定義されている以下の行でコマンドを利用。その関数、クラスが畳まれてファイルの見通しが良くなる。
- `command + F`：で文字を探し、FindをReplaceに変えて、変更したい文字列を入力すれば文字変換ができる
- `command + B` : ビルドすることでコードの変更を反映
- `command + Q`：シュミレーターを消す。
- `commnad + R`：buildしてシュミレーターを立ち上げる。
- `commnad + .`：アプリが停止
- `command + shift + K`：プロジェクトをクリーン。フレームワークの反映が遅れていたり、何かおかしかったりするときにこのショートカットを使えば改善されたりする
- `command + shift + L`：storyBoardでオブジェクトウィンドウが立ち上がる
- `command + option + control + enter`：ストーリボードを選択してこのショートカットを打つと、そのstoryBoardに関連するviewControllerが二分割に表示される
- `command + control + e`：選択した変数が使われているところを一斉に変換する
- `command + shift + y`：下のウィンドウを開いたり、閉じたりできる
- `command + 0`：左側のウィンドウの表示非表示
- `command + option + 0`：右側のウィンドウの表示非表示
- `command + 1, 2, 3…`：左側ウィンドウで何を表示するか選択できる
- `command + control + → or ←`：前開いていたファイルに戻ったりできる
- `command + shift + O`：プロジェクト内のファイルを検索してそのファイルに移動できる
- `command + control + j`：変数や関数の宣言場所がわかる
- `command + s`：シュミレータのスクショができる
- `command + shift + H`：シュミレータでホーム画面に戻る

### Finder
- `command + option + space`：Finder を開く
- `command + shift + G` : filePathを入力できるようになり、pathがわかれば該当の箇所まで飛べる
- `command + ↑` : 下位層のディレクトリに移動。例えば、ホームディレクトリからこれを使っていくことによって、一番最下層のMacintosh HDまで移動できる。

### Mac
- 音量
  - `fn + f10`：ミュート
  - `fn + f11`：音量を下げる
  - `fn + f12`：音量を上げる

- 画面の明るさ
  - `fn + f1`：暗く
  - `fn + f2`：明るく

- `command + shift + space`：絵文字を開く

### 最後に
他にこんなショートカットがあって便利だよ！などがございましたら是非教えていただきたいです。