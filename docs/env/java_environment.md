---
title: Java のセットアップ
description: Java を扱う上で必要となる環境をセットアップします。
author: tick-taku
---

# Java のセットアップ

Android アプリ開発を行うために Java が動く必要があります。ここでは Java のセットアップから Android Studio でビルドできるまでの環境構築を行います。

**macOS でのセットアップしか説明していません！[Homebrew](https://brew.sh/index_ja) がインストールされているか確認してください。** またシェルは [zsh](https://zsh.sourceforge.io/Arc/source.html) を想定していますがおそらく何でも大丈夫だと思います。

## Java に関連する用語集

セットアップを行う前に Java を触る上で必要な単語を理解しておきましょう。ちなみに `OpenJDK` は Java のオープンソース版みたいなものです。

- [Android の実行環境 - Qiita](https://qiita.com/tick-taku/items/ea3dd528030f4992b64d)

## Java のインストール

**Android 開発に必要になるのは Java 11** なので `openjdk11` をインストールします。以下の流れで進めていきます。

1. インストールする openjdk の情報を見てみましょう。
2. `openjdk11` をインストールしてみましょう。
3. `openjdk11` のシンボリックリンクを作成する
4. `openjdk11` の PATH を通す
5. 動作確認

### インストールする openjdk の情報を見てみましょう

```zsh
$ brew search openjdk

==> Formulae
openjdk@11                         openjdk ✔                          openjdk@17                         openjdk@8

==> Casks
openttd
```

今インストールできる openjdk がリストアップされますが、今回必要なのは `openjdk11` なのでバージョンを指定して見てみます。

```zsh
$ brew info openjdk@11

==> openjdk@11: stable 11.0.18 (bottled) [keg-only]
Development kit for the Java programming language
https://openjdk.java.net/
Not installed
From: https://github.com/Homebrew/homebrew-core/blob/HEAD/Formula/openjdk@11.rb
License: GPL-2.0-only
==> Dependencies
Build: autoconf ✔, pkg-config ✔
Required: giflib ✔, harfbuzz ✘, jpeg-turbo ✔, libpng ✔, little-cms2 ✔
==> Caveats
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk

openjdk@11 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
```

`openjdk11` がインストールできることが確認できましたね。

### `openjdk11` をインストールしてみましょう

```zsh
$ brew install openjdk@11

==> openjdk@11
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk

openjdk@11 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

If you need to have openjdk@11 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openjdk@11/bin:$PATH"' >> ~/.zshrc
```

無事インストールできたら最後の方に表示されているメッセージを確認してみましょう。

まず info の時点でも出ていたと思いますが `openjdk@11 is keg-only` と表示されていると思います。[`keg-only` とは **インストールのみでシンボリックリンクは作成しない**設定です](https://zenn.dev/fujishiro/scraps/d311a91daccb1d)。シンボリックリンクはファイルやディレクトリへのエイリアスのようなものです。

続いて PATH を通しましょうと言うメッセージが表示されています。PATH を通さないとコマンドを実行しても対応するプログラムを探せません。

なのでまずはこの2つを対応しましょう。

### `openjdk11` のシンボリックリンクを作成する

シンボリックリンクの作成のコマンドはメッセージの下に表示されていますのでそれを実行しましょう。

```
$ sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
```

### `openjdk11` の PATH を通す

こちらも何をするかが表示されています。以下の PATH を zshrc に追記しましょう。bash の場合は bashrc です。たぶん。もし zshrc がない場合は echo を出力するコマンドが表示されているのでそれを実行してください。

```
export PATH="/opt/homebrew/opt/openjdk@11/bin:$PATH"
```

### 動作確認

設定ファイルを読み込みなおして JDK の `java` コマンドを入力してみましょう。バージョンを確認してみて info で表示されたものと一致していれば成功です。

```
$ source ~/.zshrc
$ java --version

openjdk 11.0.18 2023-01-17
OpenJDK Runtime Environment Homebrew (build 11.0.18+0)
OpenJDK 64-Bit Server VM Homebrew (build 11.0.18+0, mixed mode)
```

