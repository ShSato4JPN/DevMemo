#  StyleLint とは
[StyleLint](https://stylelint.io/)

[.stylelintrc(Qitta)](https://qiita.com/takeshisakuma/items/a7a3b8cc0ce05422f686)

[prettier, eslint, stylelint について](https://rinoguchi.net/2021/12/prettier-eslint-stylelint.html)

StyleLint は eslint の CSS、SCSS 版。

プラグインを追加することで、ルールの追加等を容易に行うことが可能。

config ファイルは、JSON、YAML、JAVASCRIPT に対応している。

# prettier, eslint, stylelint の共存について
[prettier, eslint, stylelint について](https://rinoguchi.net/2021/12/prettier-eslint-stylelint.html)

上のサイトにちょうどいい内容でまとめられていた。

- 一般的な開発では、Prettier でフォーマットする。（ファイル保存時に自動フォーマットする）
- 言語毎のコード構造に関する問題（JavaScript や TypeScript） については ESLint で対応。
- CSS や SCSS については StyleLint でリント＆フォーマットする

**※※※ ポイント ※※※**

Prettier と競合するルールは無効化する。

エディター上でリント結果のワーニングやエラーを表示する。

ファイル保存時に自動フォーマットする。

# StyleLint　のインストール
```
//lintのみ
npx stylelint src/css/**/**.css
npx stylelint src/scss/**/**.scss

//lint + 自動修正
npx stylelint src/css/**/**.css --fix
npx stylelint src/scss/**/**.scss --fix
```

|ルールセット名|内容|
|-|-|
|stylelint-config-recommended|最小限のCSSのルールセット|
|stylelint-config-standard|一般的なCSSのルールセット|
|config-recommended-scss|SCSSのルールセット|
|stylelint-config-primer|GitHubのCSSのルールセット|
|stylelint-config-wordpress|WordPressのルールセット|
|stylelint-config-twbs-bootstrap|Bootstrapのルールセット|

上のルールを適用するには、npm install -D を実行後、.stylelintrc ファイルにプラグインの記述を行う。

css の基礎がないと記述が難しいそう。。。

```
{
  "extends": [
    "stylelint-config-standard-scss",
    "stylelint-config-standard",
    "stylelint-config-css-modules",
    "stylelint-config-recommended-scss",
    "stylelint-config-sass-guidelines",
    "stylelint-config-prettier"
  ],
  "plugins": ["stylelint-order", "stylelint-scss"],
  "rules": {
    "at-rule-no-unknown": null,
    "color-named": [
      "never",
      {
        "ignore": ["inside-function"]
      }
    ],
    "function-no-unknown": [
      true,
      {
        "ignoreFunctions": ["map.get"]
      }
    ],
    "order/properties-alphabetical-order": true,
    "property-no-unknown": [
      true,
      {
        "ignoreProperties": ["desktop", "mobile", "tablet", "wide"]
      }
    ],
    "scss/at-rule-no-unknown": [
      true,
      {
        "ignoreAtRules": ["value"]
      }
    ],
    "selector-class-pattern": null,
    "selector-pseudo-class-no-unknown": [
      true,
      {
        "ignorePseudoClasses": ["export", "global"]
      }
    ]
  }
}
```