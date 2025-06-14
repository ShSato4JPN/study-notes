# 便利なツール

## ◾️ postCSS

・PostCSSは、CSSを処理するためのツールで、プラグインを使用してCSSを変換、最適化、拡張することができる。（Tailwind CSSはPostCSSのプラグインとして動作し、ユーティリティファーストなCSSフレームワークを提供する。）

・postCSS ただのCSSを処理するツールなのでプラグインを使用しないと何もできない。

## ◾️ tailwind

Tailwind CSSは、ユーティリティファーストなCSSフレームワークで、PostCSSのプラグインとして動作する。Tailwindを使用すると、事前に定義されたクラスを使用して迅速にスタイリングを行うことができる。

HTML や JSX ファイルの中で使用されているクラスを解析し、実際に使用されているクラスのみを含むCSSファイルを生成している。

## ◾️ tailwindとpostCSSの連係

>　1. global.css を読み込む
>　↓
>　2. Tailwind CSS プラグインが発動
>　   - tailwind.config.ts を参照して、カスタム設定を取得
>　   - content プロパティで指定されたファイルをスキャン
>　   - 使用されているクラスに対応するCSSを生成
>　↓
>　3. Autoprefixer プラグインが発動（オプション）
>　   - display: flex → -webkit-flex など、古いブラウザ対応のプレフィックスを追加
>　↓
>　4. 最終的なCSSファイルを出力

## ◾️ まとめ

Tailwind CSSはPostCSSのプラグインとして動作し、ユーティリティファーストなスタイリングを提供する。PostCSSはCSSを処理するためのツールであり、Tailwindはその上で動作することで、効率的なスタイリングを実現している。Tailwindの設定や使用されているクラスに基づいて、必要なCSSのみを生成するため、パフォーマンスも向上する。

Autoprefixer は、PostCSSのプラグインであり、CSSの互換性を向上させるために使用される。Tailwind CSSとAutoprefixerを組み合わせることで、最新のブラウザと古いブラウザの両方で適切にスタイルが適用されるようになる。

## ◾️ 参考リンク

- [Tailwind CSSの公式ドキュメント](https://tailwindcss.com/docs/installation)
- [PostCSSの公式ドキュメント](https://postcss.org/)
- [Autoprefixerの公式ドキュメント](https://github.com/postcss/autoprefixer)
