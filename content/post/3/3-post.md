---
title: "fvm flutter doctor：! Warning: `dart` on your path resolves to /usr/local/Cellar/dart/2.19.5/libexec/bin/dart, which is not inside your current Flutter SDK ~ の解決策"
date: 2023-05-10T08:12:58+09:00
draft: false
tags: ["Flutter", "ターミナル"]
categories: ["Flutter"]
---

`fvm flutter doctor`を実行した際に、pathに関する警告が出て困った経験があったので、その解決策を示す。

警告内容は以下の通り。
```
$ fvm flutter doctor
Doctor summary (to see all details, run flutter doctor -v):
[!] Flutter (Channel stable, 3.7.8, on macOS 12.5.1 21G83 darwin-arm64 (Rosetta), locale ja-JP)
    ! Warning: `dart` on your path resolves to /usr/local/Cellar/dart/2.19.5/libexec/bin/dart, which is not inside your current Flutter SDK checkout at /Users/ka_mori/fvm/versions/3.7.8. Consider adding /Users/ka_mori/fvm/versions/3.7.8/bin to the front of your path.
[✓] Android toolchain - develop for Android devices (Android SDK version 33.0.0)
[✓] Xcode - develop for iOS and macOS (Xcode 14.2)
[✓] Chrome - develop for the web
[✓] Android Studio (version 2022.1)
[✓] VS Code (version 1.77.3)
[✓] Connected device (4 available)
[✓] HTTP Host Availability
```

上記のエラーは、システムの `PATH` に設定されている `dart` コマンドが、現在の Flutter SDK 内に存在しないために発生している。

`fvm flutter doctor` を実行した際に、`dart` コマンドのパスが適切に設定されていない場合に警告が表示される。これは `FVM` の問題ではなく、Flutter がシステムの `dart` コマンドのパスと、FVM で選択された Flutter SDK 内の `dart` コマンドのパスを比較しているため生じるものである。

`fvm flutter doctor` と `flutter doctor` は、基本的に同じ操作を実行するため、どちらのコマンドを使っても、選択された Flutter バージョンでコマンドが実行される。

そのため、警告を表示させたくない場合は、`flutter doctor` を使って問題ない。

### なぜ警告が出るのか？
警告が表示される理由は、システムの `PATH` で見つかる `dart` コマンドが、FVM で選択された Flutter SDK 内の `dart` コマンドではなく、別の場所にあるため。これが `fvm flutter doctor` で警告が表示される原因である。

`fvm flutter doctor` を実行した際の、警告の流れは以下の通り。
1.  FVM は選択された Flutter バージョン（この場合は `/Users/ka_mori/fvm/versions/3.7.8`）を使って `flutter doctor` コマンドを実行。
2.  `flutter doctor` は、`PATH` に設定された `dart` コマンドの場所をチェックする。この場合、`/usr/local/Cellar/dart/2.19.5/libexec/bin/dart` が最初に見つかる。
3.  次に、`flutter doctor` は、選択された Flutter SDK 内の `dart` コマンドの場所をチェックする。この場合、`/Users/ka_mori/fvm/versions/3.7.8/bin/dart`。
4.  `flutter doctor` は、2 と 3 で見つかった `dart` コマンドの場所が異なることに気づき、警告を表示する。

しかし、実際には `fvm` を使って選択された Flutter バージョンを実行する際、`PATH` に設定された `$HOME/fvm/default/bin` が使用されている。これは、`/Users/ka_mori/fvm/default -> /Users/ka_mori/fvm/versions/3.7.8` へのシンボリックリンクである。したがって、警告は無視しても問題ない。

### `/usr/local/Cellar/dart/2.19.5/libexec/bin/dart` この PATH はどこで設定した？
`/usr/local/Cellar/dart/2.19.5/libexec/bin/dart` は、Homebrew 経由でインストールされた Dart のパスである。恐らく以前に Homebrew で Dart をインストールしたことがあるか、何らかの理由でこのパスが設定された可能性がある。
`brew list` で確認できる。

ただし、警告を完全に消す方法として、Homebrew でインストールされた Dart をアンインストールすることができる。
`$ brew uninstall dart`

### Homebrew でインストールしたパッケージは、`/usr/local/bin` や `/usr/local/opt` ディレクトリに格納されており、macOS はデフォルトで `/usr/local/bin` がシステムの `PATH` に含まれている
つまり、homebrew で入れたものは自動的に path に設定される。
これにより、ターミナルでそのパッケージのコマンドをすぐに実行できるようになる。

### `/usr/local/Cellar/dart/2.19.5/libexec/bin/dart` は、`/usr/local/binや/usr/local/opt` にも入ってなくないか？
`/usr/local/Cellar/dart/2.19.5/libexec/bin/dart` は、実際には `/usr/local/bin` や `/usr/local/opt` には含まれていない。ただし、`Homebrew` でインストールされた Dart は、通常 `/usr/local/Cellar/dart/<version>/libexec/bin` にインストールされる。

Homebrew はインストール後、シンボリックリンクを作成して、実行可能ファイルを `/usr/local/bin` にリンクする。このため、Dart コマンドを実行すると、システムの `PATH` から `/usr/local/bin` にあるシンボリックリンクを経由して、最終的に `/usr/local/Cellar/dart/<version>/libexec/bin/dart` が実行される。

システムの `PATH` には `/usr/local/bin` が含まれているため、間接的に `Homebrew` でインストールされた Dart が `PATH` に設定されているといえる。

### なぜ `/Users/ka_mori/fvm/default/bin` を先に `PATH` 設定しているのに、`/usr/local/bin` の `Dart` の方が先に見つかるのか？
1.  `PATH` には、`/Users/ka_mori/fvm/default/bin` が最初に設定されている。
2.  `which flutter` および `which dart` の結果は、FVM で選択された Flutter SDK 内の `flutter` および `dart` を示す。
3.  しかし、`fvm flutter doctor` を実行すると、警告が表示される。

この状況から、`fvm` が `flutter` コマンドをラップしていることが影響していると考えられる。`fvm` が `flutter` コマンドをラップしているため、`flutter` コマンドが内部で `dart` コマンドを呼び出す際に、システムの `PATH` が正しく解決されず、`/usr/local/bin` の `dart` が先に見つかっている可能性がある。

### dart を uninstall したが、警告が消えない
似たような別の警告が出た。
```
[!] Flutter (Channel stable, 3.7.8, on macOS 12.5.1 21G83 darwin-arm64 (Rosetta), locale ja-JP) ! Warning: `dart` on your path resolves to /opt/homebrew/Cellar/dart/2.17.5/libexec/bin/dart, which is not inside your current Flutter SDK checkout at /Users/ka_mori/fvm/versions/3.7.8. Consider adding /Users/ka_mori/fvm/versions/3.7.8/bin to the front of your path.
```

警告によると、Dart が `/opt/homebrew/Cellar/dart/2.17.5/libexec/bin/dart` にも存在していることがわかる。
なので、`/opt/homebrew/Cellar/dart/2.17.5/libexec/bin/dart` が残っている場合は、そのディレクトリを削除する。

これで `fvm flutter doctor` で警告が出なくなる！

### `/usr/local/` と `opt/homebrew` はなんだったのか？
`/opt/homebrew/` は、Apple Silicon（M1 チップ）を搭載した Mac 向けの Homebrew のインストール先である。Apple Silicon（M1）用のバイナリを提供するために、`Homebrew` は Intel Mac 向けの `/usr/local/` とは別のディレクトリ `/opt/homebrew/` にインストールされる。

Intel Mac の場合、Homebrew は `/usr/local/` にインストールされることが一般的である。しかし、Apple Silicon Mac では、`/opt/homebrew/` が使用されるため、同じシステム上で 2 つの異なるアーキテクチャのバイナリが存在することがある。

### まとめ
警告が出ていた理由は、`/opt/homebrew`, `/usr/local/` のどちらのディレクトリにも Dart がインストールされていたからである。ディレクトリを削除することで問題が解決したが、今後同様の問題が発生しないよう、使用しているツールのアーキテクチャには注意していきたい。

