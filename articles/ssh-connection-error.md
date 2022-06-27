---
title: "Bad configuration option: ssh-rasa..."
emoji: "🐱"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["ssh"]
published: true
---

GitHubとのssh接続ができているか確認するためのコマンド
```shell
$ ssh -T git@github.com
```
を打つと以下のエラーが起きる場合がある。

```shell
/Users/yoshikitanaka/.ssh/config: line1: Bad configuration option: ssh-rsa
/Users/yoshikitanaka/.ssh/config: terminating, 1 bad configuration options
```

今回の場合は鍵の設定をすれば解決しそうであったので、鍵の設定方法を2通り紹介する。

1つ目が
```shell
~.ssh/config（ファイル名）
```
に
```shell
IdentityFile 鍵へのPATH（例：~/.ssh/id_rsa）
```
という1行を追加するか方法。

2つ目が
```shell
$ ssh-add 鍵へのPATH（例：~/.ssh/id_rsa ）
```
で直接鍵を指定する方法。

今後のためを考えると1つ目の方法を選んで、~/.ssh/configの使い方に慣れる方が良さそう。
以下に参考になりそうな記事を載せておく。
- https://qiita.com/passol78/items/2ad123e39efeb1a5286b
- https://web.kudpc.kyoto-u.ac.jp/manual/ja/install/ssh-add