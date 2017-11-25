# About This

Serverless Framework + TypeScriptでAPI Gatewayを作成するサンプル。
Serverless Frameworkを作業フォルダにインストールするため、通常の手順とは異なる。

# 作成手順

## Serverless Frameworkのインストール
```
$ npm install serverless

$ ./node_modules/.bin/serverless --version
1.24.1
```

## テンプレート作成
```
$ ./node_modules/.bin/serverless create -t aws-nodejs-typescript
```

package.jsonにServerless Frameworkを追記。(これを行わなと次のコマンドでローカルにインストールしたServerless Frameworkが消えるため)
package.jsonに記載されたライブラリをインストール。

```
$ npm install
```

## serverless.ymlの編集
providerに以下を追加。
```
provider:
  (中略 ここはデフォルト)
  stage: dev
  region: ap-northeast-1
  profile: default
```

## デプロイ

デプロイしようとすると以下のエラーが発生する。

```
Cannot find name 'AsyncIterator'.
```

tsconfig.jsonのcompilerOptionsに以下を追加する。
```
"lib": ["es6", "dom", "esnext"]
```

※参考サイト[Cannot find name 'AsyncIterator' error in Typescript compilation process.](https://github.com/apollographql/graphql-subscriptions/issues/83#issuecomment-326675684)

上記を追加した後でデプロイ。

```
$ ./node_modules/.bin/serverless deploy
```

# 参考サイト

* https://gregshackles.com/getting-started-with-serverless-and-typescript/
* https://serverless.com/framework/docs/providers/aws/cli-reference/create/
* https://serverless.com/framework/docs/providers/aws/guide/serverless.yml/
* https://github.com/apollographql/graphql-subscriptions/issues/83#issuecomment-326675684
* https://qiita.com/sinmetal/items/395edf1d195382cfd8bc
