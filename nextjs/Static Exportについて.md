# Static Exportについて

[公式ドキュメントより](https://nextjs.org/docs/pages/guides/static-exports)

## How to create a static export of your Next.js application

Next.jsアプリケーションの静的エクスポートの作成方法
Next.jsは、静的サイトまたはSPA（Single-Page Application）として開始し、その後オプションでアップグレードして、サーバーを必要とする機能を使用することができます。

次のビルドを実行すると、Next.jsはルートごとにHTMLファイルを生成します。Next.jsは、厳密なSPAを個々のHTMLファイルに分割することで、クライアントサイドでの不要なJavaScriptコードの読み込みを回避し、バンドルサイズの縮小とページロードの高速化を実現します。

Next.jsはこの静的エクスポートをサポートしているので、HTML/CSS/JSの静的アセットを提供できるウェブサーバーであれば、どこにでもデプロイしてホストすることができます。

``` javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export',
};

export default nextConfig;
```

自身のサイトに Static Export の設定を入れてビルドしてみたところエラーが発生した。

どうも、動的ルーティング時に渡されるパラメータが不明確でエラーになったっぽい。

公式ドキュメントいわく、generateStaticParams を使うことで、動的ルーティングのパラメータを明示的に指定することができる。
