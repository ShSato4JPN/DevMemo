## 1. Next プロジェクト作成

[Next-craete-app](https://nextjs.org/docs/api-reference/create-next-app#non-interactive)

```
npx create-next-app@latest --ts --use-npm
```

## 2. renovate の設定

[renovate](https://docs.renovatebot.com/)

```
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "assignees": ["ShSato4JPN"],
  "reviewers": ["ShSato4JPN"],
  "extends": ["config:base"],
  "timezone": "Asia/Tokyo",
  "packageRules": [
    {
      "automerge": true,
      "groupName": "devDependencies",
      "matchDepTypes": ["devDependencies"],
      "matchUpdateTypes": ["minor", "patch", "pin", "digest"]
    },
    {
      "automerge": true,
      "groupName": "dependencies",
      "matchDepTypes": ["dependencies"],
      "matchUpdateTypes": ["minor", "patch", "pin", "digest"]
    }
  ],
  "platformAutomerge": true,
  "schedule": ["every weekend"]
}

```

## 3. eslint の導入

[eslint](https://eslint.org/docs/latest/use/getting-started)

```
npm init @eslint/config
```

```
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@next/next/recommended",
    "next/core-web-vitals",
    "prettier"
  ],
  "overrides": [],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "plugins": ["react", "@typescript-eslint"],
  "rules": {
    "react-hooks/exhaustive-deps": [
      "error",
      {
        "enableDangerousAutofixThisMayCauseInfiniteLoops": true
      }
    ]
  }
}

```

## ４. Sass

[Next-Sass](https://beta.nextjs.org/docs/styling/sass)

```
npm install --save-dev sass
```

## 5. stylelint の導入

[stylelint](https://stylelint.io/user-guide/get-started)

```
npm init stylelint,,
npm install stylelint-config-css-modules // css-modules を使用する場合
```

```
{
  "extends": ["stylelint-config-standard", "stylelint-config-css-modules"],
  "rules": {
    "selector-class-pattern": null,
    "color-no-invalid-hex": true,
    "function-calc-no-invalid": true,
    "function-calc-no-unspaced-operator": true,
    "string-no-newline": true,
    "declaration-block-no-duplicate-properties": true,
    "declaration-block-no-shorthand-property-overrides": true
  }
}

```

## commitlint の導入

[commitlint](https://commitlint.js.org/#/?id=getting-started)

```
npm install @commitlint/cli @commitlint/config-conventional
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

## husky の導入

[husky](https://github.com/typicode/husky)
[lint-staged](https://github.com/okonet/lint-staged)

```
npm install husky
npm install lint-staged
```

package.json に追加

```
  "prepare": "husky install",
  "lint-staged": "lint-staged"
```

npm scripts 実行

```

npm run prepare
```

自動生成される `.husky` フォルダの直下に以下のファイルを作成する

- `commit-msg`

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx --no -- commitlint --edit ${1}

```

- `pre-commit`

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged

```

プロジェクトのルートに `lintstagedrc.js` を作成する

- `lintstagedrc.js`

```
module.exports = {
  "*": "prettier --ignore-unknown --write",
  "**/*.scss": "stylelint --fix",
  "**/*.ts?(x)": "eslint --fix",
};

```

#### 🚨 githooks が動かない場合は `husky` フォルダ直下のファイルに実行権限が付与されていない場合があるので以下のコマンドを実行する。

```
// ug+x は、ユーザ、グループに実行権限与えるオプション
chmod ug+x .husky/*
```

husky の公式ドキュメント通り、スクリプトを使ってファイルを作成すると実行権限が付与される

```
npx husky add .husky/commit-msg "npm test"
```

👇

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npm test

```

✨ 追記 ✨

husky で使用するファイルはこちらのコマンで叩くだけでおっけい！

```
npx husky add .husky/commit-msg "npx
--no -- commitlint --edit ${1}"
npx husky add .husky/pre-commit "npx lint-staged"
```
