# lint-staged とは
[lint-staged](https://github.com/okonet/lint-staged)

husky に hook させる lint を設定する。

npm script に `"lint-staged": "lint-staged"` を追加後、

husky の pre-commit に `npm run lint-staged`を追加する。

※　手作業でも追加は可能だが、下のコマンドを使って husky を使って追加するのがいいかも。
```
npx husky add .husky/pre-commit "npm run　〇〇〇"
```

基本的には、`lint-staged` を実行すればプロジェクト roor の `.lintstagedrc.js ` が実行される。

`.lintstagedrc.js ` の設定は以下の通りでよい。

```
module.exports = {
  "*": "prettier --ignore-unknown --write",
  "**/*.scss": "stylelint --fix",
  "**/*.ts?(x)": "eslint --fix",
};
```

[next.js の公式ドキュメント](https://nextjs.org/docs/basic-features/eslint)にも設定方法が載っているが、上の設定でちゃんと動くので問題ない。
