---
title: "Serverless Frameworkを使ってLambda + API Gateway + DynamoDBの環境を構築してみる"
emoji: "🐱"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Serverless Framework", "AWS", "Lambda"]
published: true
---

## 目次
1. Serverlessのインストール
2. サービスの作成
3. サービスをデプロイしてみる
4. API Gatewayの設定
5. DynamoDBの設定
6. まとめ

## 1. Serverless Frameworkのインストール
Serverlessはnpmのパッケージとして公開されているため、ターミナルより以下を打つとグローバルにインストールされる。
```shell
$ npm install -g serverless
```

正しくインストールできているか<span style="color: #6c737b"><span style="color: #1453c6">serverless --version</span>と打って以下の表示になっているかどうかで確認できる。
```shell
$ serverless --version
Framework Core: 2.72.3 (local)
Plugin: 5.5.4
SDK: 4.3.2
```
## サービスの作成

Serverlessではサービスという単位で実行環境を構築しているらしい。
    
 そして実際にサービスを構築するためには以下をターミナルで打てば良い。
 ```shell
 $ serverless create --template aws-nodejs --name my-special-service --path my-special-service
 ```
    
 すると以下のようなディレクトリ群が作成される。
 ```
 - my-special-service
     - .gitignore
     - handler.js
     - serverless.yml
```
ここで、グローバル（自分の場合だと/usr/local/lib/）にserverlessを置いた状態だとエラーが起きることがあるため、
    my-special-service階層でもう一度serverlessをインストールする。
```shell
$ cd my-special-service
 ```
```shell
$ npm install serverless
```
すると以下のようなディレクトリ群が作成される。
 ```
 - my-special-service
     - .serverless
     - node_modules
     - .gitignore
     - handler.js
     - package-lock.json
     - package.json
     - serverless.yml
```
    
以下にそれぞれのファイルの詳細を記載する。

### .serverless
serverlessライブラリ群。基本いじることがないと思う。
    
### serveless.yml
サービス全体の設定を行うためのファイル。
ここを書き換えることでそれぞれの環境構築が可能になる。
    
### hander.js
Lambdaで実行する関数をここに記載していく。
    
### package.json/package-lock.json/.gitignore
省略
    
## サービスをデプロイしてみる
ここで作成したサービスをプロバイダー上へデプロイしてみる。
デプロイするためには以下をターミナル上で打てば良い。

```shell
$ serverless deploy -v 
```

-vオプションを付けるとverboseというモードでデプロイが実施され、途中経過がターミナル上で確認できる。

ここまででLambdaの関数を構築・デプロイまで完了したので、プロバイダーのLambdaの関数画面から確認すると良い。

## API Gatewayの設定
    
API Gatewayを設定するためには以下をserverless.ymlに加える。
```
# Lambdaのイベントトリガーを設定
events:
# トリガーとしてAPIGatewayを構築
  - http:
    path: sample/test # リソースを指定
    method: post # メソッドを指定
    integration: lambda # 統合サービスをLambdaにする
```
一旦デプロイするために以下をターミナルに打つ。
```shell
$ serverless deploy -v 
```
ここまででAPI Gatewayを構築・デプロイまでが完了したので、プロバイダーのLambdaの関数画面から確認すると良い。
    
## DynamoDBの設定
```
# リソースの構築
resources:
  Resources:
    # DynamoDBの構築
    DynamoDbTable:
      Type: 'AWS::DynamoDB::Table'
      Properties:
        # キーの型を指定
        AttributeDefinitions:
          -
            AttributeName: id
            AttributeType: S
            -
            AttributeName: name
            AttributeType: S
```
ここまででDynamoDBを構築・デプロイまでが完了したので、プロバイダーのDynamoDBの画面から確認すると良い。

## 参考文献
- https://serverless.co.jp/blog/25/
- https://qiita.com/t_okkan/items/546330b5f4da720c71a7
