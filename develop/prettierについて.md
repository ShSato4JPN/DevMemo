# prettier とは
[Prettier](https://prettier.io/)

ソースコードを自動成形してくれるツールのこと。

EditorConfig はエディタの制御を統一化するツールに対して、Prettier はコーディングのフォーマットを統一化するツール。

今回は下の設定値について調査する。

```
module.exports = {
  "endOfLine": "lf",
  "semi": false,
  "singleQuote": true,
  "jsxSingleQuote": true,
  "tabWidth": 2,
  "printWidth": 60
}
```
## "endOfLine": "lf",
改行コードを指定する
## ■　semi
コードの末尾にセミコロンを付けるか付けないか
true の場合は自動で末尾にセミコロンが追加される。
## ■　singleQuote
true の場合、文字列などで使用されているダブルクォーテーションをシングルクォーテーションに自動変換する。
## ■　jsxSingleQuote
jsx 内で使用されているダブルクォーテーションをシングルクォーテーションに自動変換する。
## ■　tabWidth
タブ押下時のスペースの数を設定する。
## ■　printWidth
自動改行される文字列の長さ設定する。
公式いわく 80 以上の設定はやめた方がいいとのこと。（コードの見やすさが損なわれるため。）

コードをコミットする直前などに Prettier を使ってフォーマットを適用されるのがベスト！
