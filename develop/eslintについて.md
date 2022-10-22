#  ESLint とは
[ESLint](https://eslint.org/docs/latest/user-guide/getting-started)

ESLint は JS を静的解析してくれるツールのこと。

昨今のフロント開発では必須と言っても良い。

# ESLint のインストール
ESLint は package.json がないとインストール時にエラーとなる。

新規プロジェクトの場合は、まず npm　の初期化を行う。
```
npm init -y
```
package.json ファイル生成後、eslint のインストールを行う
```
npm init @eslint/config
```
インストール時に 3 つ選択肢が出てくる。
- 構文チェックだけ
- 構文チェックと問題のあるコードをチェック
- 構文チェックと問題のあるコードをチェックとコーディングスタイルの適用
```
? How would you like to use ESLint? … 
  To check syntax only
  To check syntax and find problems
> To check syntax, find problems, and enforce code style
```
プロジェクトで使用するモジュールの選択する。
```
? What type of modules does your project use? … 
❯ JavaScript modules (import/export)
  CommonJS (require/exports)
  None of these
```
使用するフレームワークを選択する。
```
? Which framework does your project use? … 
❯ React
  Vue.js
  None of these
```
TypeScript を使用するか選択する。
```
? Does your project use TypeScript? › No / ○Yes
```
コードをどこで実行するか選択する。
```
? Where does your code run? …  (Press <space> to select, <a> to toggle all, <i> to invert selection)
✔ Browser
✔ Node
```
プロジェクトのスタイルをどのように定義するか選択する。
```
? How would you like to define a style for your project? … 
❯ Use a popular style guide
  Answer questions about your style
```
どのスタイルを適用するか選択する。
```
? Which style guide do you want to follow? … 
❯ Standard: https://github.com/standard/eslint-config-standard-with-typescript
  XO: https://github.com/xojs/eslint-config-xo-typescript
```
フォーマットファイルのファイル形式を選択する。

 JavaScript と YAML　はファイル内にコメントを残すことができるのでおすすめ。

 YAML はコメントを記述できる JSON のようなもので、インデントを使って記述していく。
```
? What format do you want your config file to be in? … 
  JavaScript
> YAML
  JSON
```
関連するパッケージをインストールするか選択する。
```
eslint-plugin-react@latest eslint-config-standard-with-typescript@latest @typescript-eslint/eslint-plugin@^5.0.0 eslint@^8.0.1 eslint-plugin-import@^2.25.2 eslint-plugin-n@^15.0.0 eslint-plugin-promise@^6.0.0 typescript@*
? Would you like to install them now? › No / ○Yes
```
パッケージマネージャーを選択する。
```
? Which package manager do you want to use? … 
❯ npm
  yarn
  pnpm
```
インストール後に自動生成される eslintrc ファイルの内容
```
env:
  browser: true
  es2021: true
extends:
  - plugin:react/recommended
  - standard-with-typescript
overrides: []
parserOptions:
  ecmaVersion: latest
  sourceType: module
plugins:
  - react
rules: {}
```
# [参考] ESLint の設定
```
{
  "root": true,
  "extends": [
    "eslint:recommended",
    "google",
    "plugin:@typescript-eslint/recommended",
    "plugin:css-modules/recommended",
    "plugin:typescript-sort-keys/recommended",
    "next/core-web-vitals",
    "prettier"
  ],
  "ignorePatterns": ["*.d.ts", "*.js"],
  "overrides": [
    {
      "excludedFiles": ["_app.tsx", "_document.tsx"],
      "files": "*",
      "rules": {
        "filenames/match-exported": "off",
        "filenames/match-regex": "error"
      }
    }
  ],
  "parserOptions": {
    "warnOnUnsupportedTypeScriptVersion": false
  },
  "plugins": [
    "css-modules",
    "ext",
    "filenames",
    "sort-destructure-keys",
    "sort-keys-shorthand",
    "typescript-sort-keys",
    "unused-imports"
  ],
  "rules": {
    "@typescript-eslint/explicit-function-return-type": "error",
    "@typescript-eslint/no-unused-vars": "off",
    "ext/lines-between-object-properties": ["error", "never"],
    "import/newline-after-import": [
      "error",
      {
        "count": 1
      }
    ],
    "import/order": [
      "error",
      {
        "alphabetize": {
          "caseInsensitive": true,
          "order": "asc"
        },
        "warnOnUnassignedImports": true
      }
    ],
    "import/prefer-default-export": "error",
    "newline-before-return": "error",
    "no-duplicate-imports": "error",
    "no-multiple-empty-lines": [
      "error",
      {
        "max": 1
      }
    ],
    "padding-line-between-statements": [
      "error",
      {
        "blankLine": "always",
        "next": [
          "break",
          "const",
          "do",
          "export",
          "function",
          "let",
          "return",
          "switch",
          "try",
          "while"
        ],
        "prev": "*"
      },
      {
        "blankLine": "always",
        "next": "*",
        "prev": [
          "const",
          "do",
          "export",
          "function",
          "let",
          "return",
          "switch",
          "try",
          "while"
        ]
      },
      {
        "blankLine": "never",
        "next": "import",
        "prev": "*"
      },
      {
        "blankLine": "never",
        "next": "case",
        "prev": "case"
      },
      {
        "blankLine": "never",
        "next": "const",
        "prev": "const"
      },
      {
        "blankLine": "never",
        "next": "let",
        "prev": "let"
      }
    ],
    "react-hooks/exhaustive-deps": [
      "error",
      {
        "enableDangerousAutofixThisMayCauseInfiniteLoops": true
      }
    ],
    "react/jsx-boolean-value": ["error", "always"],
    "react/jsx-sort-props": "error",
    "require-jsdoc": "off",
    "semi": "error",
    "sort-destructure-keys/sort-destructure-keys": "error",
    "sort-keys": "off",
    "sort-keys-shorthand/sort-keys-shorthand": [
      "error",
      "asc",
      {
        "shorthand": "first"
      }
    ],
    "unused-imports/no-unused-imports": "error",
    "unused-imports/no-unused-vars": [
      "error",
      {
        "args": "after-used",
        "argsIgnorePattern": "^_",
        "vars": "all",
        "varsIgnorePattern": "^_"
      }
    ]
  },
  "settings": {
    "import/resolver": "node"
  }
}
```

## "root": true
> ESLint は、実行時のカレントディレクトリを起点にして、上位のディレクトリの設定ファイル (.eslintrc.\*) を探していきます。 
> 
> root: true の指定があると、この検索の振る舞いをそこで停止できます。 プロジェクトのトップディレクトリに置く .eslintrc.\* 
> 
> には、この指定をしておくとよいです。
## extends
eslint で適用するルールを追加する。
```
"extends": [
  "eslint:recommended",                       // 推奨されているチェックを全て適用する
  "plugin:@typescript-eslint/recommended",    // 既にチェックしている TS　のルールを無視する設定。↑の後に記述する
  "google",                                   // Google; のコーディングルールを適用する ※eslint-config-google
  "plugin:css-modules/recommended",           // css-module を使用する際のルールを適用する
  "plugin:typescript-sort-keys/recommended",  // TypeScript の型定義のプロパティのキーの順番を整列
  "prettier"                                  // pretteir と競合するルールを無視するため
  "next/core-web-vitals",                     // Core Web Vital のルールを追加する（SEO対策）
],
```
## ignorePatterns
eslint のルールを適用しないファイルを設定
```
"ignorePatterns": ["*.d.ts", "*.js"],  // 対象のファイル
```
## overrides
特定のファイルに個別の設定を行う場合に設定する。
```
"overrides": [
    {
      "excludedFiles": ["_app.tsx", "_document.tsx"],  // 対象外のファイル
      "files": "*",                                    // 対象のファイル
      "rules": {
        "filenames/match-exported": "off",             // ?
        "filenames/match-regex": "error"               // ?
      }
    }
  ],
```