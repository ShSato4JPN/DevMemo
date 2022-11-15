# Renovate とは
GitHub 上で動作するアプリ（bot）。

[Oinari Tech Blog](https://tech-blog.tkcco21.me/blog/manage_version_of_npm_packages/)

自動で package.json の内容を見て、古くなっているパッケージがあれば自動でプルリクエストを作ってくれるもの。

設定によっては、パッチ・マイナーアップデートはプルリクエストをまとめたり、プルリクエストを作ってくれるスケジュールを指定できたり、プルリクエストのターゲットブランチを指定できる模様。。（すごい）

こちらのサイトから renovate　のインストールと設定が可能。

https://github.com/marketplace/renovate

■ 設定の参考例
```
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "assignees": ["piro0919"],
  "dependencyDashboard": true,
  "extends": ["config:base", ":timezone(Asia/Tokyo)"],
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
  "reviewers": ["piro0919"],
  "schedule": ["every weekend"]
}
```

assignees ⇨ PR の担当者を設定

reviewers ⇨ PR のレビュアー者を設定

dependencyDashboard ⇨ v26.0.0 からデフォルトで true が設定されている。（false にする時だけ設定するで Ok）

extends ⇨ 他の linter と同じ。機能を拡張する際に設定。

packageRules ⇨ パッケージをグループ化したりして Renovate で管理する場合に利用する

platformAutomerge ⇨ プラットホームの自動マージ機能を使用するか設定。
　　　　　　　　　　　　※ 利用する際は、`Require status checks before merging` の設定が必須らしい。

schedule ⇨ Renovate をチェックさせるスケジュールを設定する。
