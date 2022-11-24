# husky とは
[husky](https://typicode.github.io/husky/#/)

 git hook をサポートするパッケージのこと。

 commit や push 前に lint したり、テストの実行などを自動で連動させてくれる。

 husky のインストールは公式ドキュメントが一番わかりやすい。

 基本的には、以下の流れでインストールを行う。

1. huksy のインストール
```
npm install husky --save-dev
```

2. npm script の追加
```
npm pkg set scripts.prepare="husky install"
```

3. script の実行
```
npm run prepare
```

すると、プロジェクトの root に .husky フォルダが生成され、そのフォルダの直下に bash ファイルが作成される。

commit 前にフックさせたいスクリプトを追加する際は下のコマンドを実行する。

```
npx husky add .husky/pre-commit "npm run　〇〇〇"
```

すると、.husky の直下に pre-commit ファイルが作成され、`npm run 〇〇〇` が末尾に追加される。


