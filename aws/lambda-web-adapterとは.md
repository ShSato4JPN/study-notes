# AWS Lambda Web Adapter とは

「Webフレームワークで作ったアプリ」を入れたコンテナを、そのままAWS Lambdaで動かせるようにするLambda拡張ツール。

## 特徴

- コンテナ化されたアプリケーションをAWS Lambdaで簡単に実行できる。
- 既存のWebフレームワーク（Express.js、Next.js、Flask、ASP.NET、Laravelなど）をそのまま利用可能。
- Lambdaのイベント駆動型アーキテクチャに対応。
- Lambdaのスケーラビリティとコスト効率を活かせる。
- Lambdaの制限（タイムアウト、メモリなど）に対応しやすい。

## 使い方

1. **コンテナイメージの作成**: Webフレームワークを使ってアプリケーションを開発し、Dockerfileを使ってコンテナイメージを作成する。
2. **Lambda関数の作成**: AWS Lambdaコンソールで新しい関数を作成し、コンテナイメージを指定する。
3. **Lambda拡張の設定**: Lambda関数の設定で、Web Adapterを有効にする。
4. **デプロイとテスト**: Lambda関数をデプロイし、API Gatewayや他のAWSサービスと連携してテストする。
