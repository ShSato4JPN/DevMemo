# Next　の環境変数について
[environment-variables](https://nextjs.org/docs/basic-features/environment-variables)

Next.js には 3 種類の環境変数定義用のファイルが存在する。

|ファイル名|読み込まれるタイミング|
|-|-|
|.env.local|毎回|
|.env.development|next dev 時のみ|
|.env.production|next start 時のみ|

表に書いてある通り、開発モード、本番モード、その両方と使い分けることができる。

さらに、Next.js には環境変数をブラウザに表示される機能も存在する。

基本的には環境変数はブラウザに表示することができない。

しかし、環境変数の頭に `NEXT_PUBLIC_` プレフィックを追加することで、

環境変数をブラウザに表示することができる。

`NEXT_PUBLIC_` を付けずにブラウザに表示しようとするとエラーになる。

⇨　ビルドエラーにはならない。。

Next のプロジェクトではないけど、Next の機能を使って読み込む場合。

https://github.com/intercom/contentful-typescript-codegen/issues/104#issuecomment-1209970799