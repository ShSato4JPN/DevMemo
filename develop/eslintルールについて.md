## import を自動的に並べ替えてくれる設定

```
"import/order": [
      "error",
      {
        "groups": [
          "builtin",
          "external",
          "parent",
          "sibling",
          "index",
          "object",
          "type"
        ],
        "pathGroups": [
          {
            "pattern": "{react,react-dom/**,react-router-dom}",
            "group": "builtin",
            "position": "before"
          },
          {
            "pattern": "@src/**",
            "group": "parent",
            "position": "before"
          }
        ],
        "pathGroupsExcludedImportTypes": ["builtin"],
        "alphabetize": {
          "order": "asc"
        },
        "newlines-between": "always"
      }
    ],
    "@typescript-eslint/consistent-type-imports": [
      "error",
      { "prefer": "type-imports" }
    ],
```

---

## React 推奨ルール

[source](https://ja.reactjs.org/docs/hooks-rules.html)

```
"react-hooks/exhaustive-deps": [
      "error",
      {
        "enableDangerousAutofixThisMayCauseInfiniteLoops": true
      }
    ]
```

---

## 使用していないパッケージを削除する

[unused-imports](https://github.com/sweepline/eslint-plugin-unused-imports)

```
{
	"plugins": ["unused-imports"]
}
```

```
{
	"rules": {
		"no-unused-vars": "off", // or "@typescript-eslint/no-unused-vars": "off",
		"unused-imports/no-unused-imports": "error",
		"unused-imports/no-unused-vars": [
			"warn",
			{ "vars": "all", "varsIgnorePattern": "^_", "args": "after-used", "argsIgnorePattern": "^_" }
		]
	}
}
```
