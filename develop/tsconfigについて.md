# tsconfig とは
[tsconfig](https://www.typescriptlang.org/ja/tsconfig) 公式ドキュメント

[ryokkkke](https://ryokkkke.com/typescript/tsconfig-json/compiler-options/isolated-modules) わかりやすくまとめられているサイト

tsconfig は TypeScript の細かい設定を行うファイルである。

今回は下の設定値について調査する。
全て覚えるの馬鹿らしいので軽く概要だけ調べる。

```
{
  "compilerOptions": {
    "allowJs": true,
    "baseUrl": "src",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "incremental": true,
    "isolatedModules": true,
    "lib": ["dom", "dom.iterable", "esnext"],
    "module": "esnext",
    "moduleResolution": "node",
    "noEmit": true,
    "resolveJsonModule": true,
    "skipLibCheck": true,
    "strict": true,
    "target": "es5"
  },
  "exclude": ["node_modules"],
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"]
}
```

## compilerOptions
TypeScript の設定のきも。

TypeScript の振る舞いを設定する項目。
## "allowJs": true,
.ts、.tsx ファイルをに対して ｡js ファイルのインポートを許可する
## "baseUrl": "src",
絶対パスのルートを指定（src を TS のルートとする）

相対パスだとファイル構成が変わったときにパスの設定が面倒臭いが、

絶対パスだと柔軟に対応できるようになる
## "esModuleInterop": true,
CommonJS 形式のモジュールを ES Modules でデフォルトインポート可能にする。
## "forceConsistentCasingInFileNames": true,
ファイルのインポート時に大文字小文字を明確に判別する。
## "incremental": true,
以前のコンパイル結果と実行したコードの差分を検出して、必要なファイルだけをコンパイルするようになる。
## "isolatedModules": true,
コンパイル対象のファイルの依存関係を無視して全てのファイルを独立したものとしてコンパイルする。
## "lib": ["dom", "dom.iterable", "esnext"],
コンパイル時に使用する組み込みライブラリを指定する。（よくわからん）
- dom →　
- dom.iterable →　
- esnext →　
## "module": "esnext",
コンパイラに適したバージョンを決めてもらう設定っぽい
## "moduleResolution": "node",
tsc のモジュールの解決方法を指定する。（あまり設定の必要がないらしい）
## "noEmit": true,
コンパイル結果を出力しない。（true） 

tsc の型チェックのみを行いたい場合に設定するとのこと。
## "resolveJsonModule": true,
JSON のインポートを可能にする設定。
## "skipLibCheck": true,
型定義ファイルのチェックをスキップする設定。

型システムの精度を犠牲にすることで、コンパイル時間を短縮する。
## "strict": true,
TypeScript の基本的なチェクを全て有効にする設定。（必須）
## "target": "es5"
トランスパイルするバージョンを設定する。

現在は ES6 がベストらしい。
## "exclude": ["node_modules"],
TypeScript のチェック対象外のフォルダやファイルを設定する。
## "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"]
TypeScript　のチェック対象とするファイルを設定する。