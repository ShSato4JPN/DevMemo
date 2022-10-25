# npm のおさらい
## dependencies と devDependencies の違い
npm はパッケージのインストール時に、本番環境用、開発環境用とでインストールする場所を分ける事ができる。

### dependencies

開発、本番環境の両方で利用するパッケージをインストールする場所。

以下のコマンドを実行すると、dependencies に記述されたパッケージのみがインストールされる。
```
npm install --production
// 同じ意味
npm install
```
### devDependencies
　
開発環境でのみ利用するパッケージをインストールする場所。（モジュールバンドラや lint 系のパッケージなど）

# パッケージのバージョンについて
パッケージに大きく分けて 3 つのバージョンが存在する。
```
  "axios": "^1.1.3"
```
左の数字から、**メジャーバージョン.マイナーバージョン.バッチバージョン** となっている。
- メジャーバージョン　⇨　互換性を保証しない、1つ以上の破壊的な変更が行われた際にカウントされる。
- マイナーマージョン　⇨　後方互換性があり、機能を追加した時などにカウントされる。
- パッチバージョン　　⇨　後方互換性があり、バグなどが修正された時などにカウントされる。

npm では、バージョンアップの許容を記号を使って設定する。

- ^(キャレット)　⇨ メジャーバージョンまでの挙動を保証 ( 3.x.x メジャーバージョン以外は更新を許可する
- ~(チルダ)　　　⇨ マイナーバージョンまでの挙動を保証 ( 3.1.x パッチバージョンの更新を許可する
- 記述なし   　　⇨ バージョン固定

# npmrc　ファイルについて
npm config set 〇〇 にて設定可能。

npm config set を行うとカレントディレクトリではなく、~/.npmrc にファイルが生成され内容が反映される動きとなる。

■ 実行例
```
// インストールするパッケージのバージョンを固定する  
npm config set save-exact=ture
```

今回参考にする設定値の役割は以下の通り。
```
also=dev
engine-strict=true
progress=false
save-exact=true
```

## ■　also=dev
shrinkwrap、outdated、update コマンドを実行するときに devDependencies を含めるようにする設定。

基本的にパッケージをアップデートする際は、開発環境のものを上げると思うので、この設定を入れておくのが無難である。
## ■　engine-strict=true
こちらの設定を入れておくことで、実行する Node のバージョンを固定する事ができる。

package.json に以下の設定を入れて、engine-strict=true を設定することで、Node 14 以外で実行しようとするとエラーにできる。
```
  "engines": {"node": "14.x"},
```
ちなみに、engine-strict=true を入れない場合、警告だけとなりあまり意味をなさない。

engine-strict=true を入れなかった場合 ⇨ インストールされた。。。
```
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: 'npm-test@1.0.0',
npm WARN EBADENGINE   required: { node: '14.x' },
npm WARN EBADENGINE   current: { node: 'v16.13.2', npm: '8.1.2' }
npm WARN EBADENGINE }
```

engine-strict=true を入れた場合　⇨ エラーになった！
```
npm ERR! code EBADENGINE
npm ERR! engine Unsupported engine
npm ERR! engine Not compatible with your version of node/npm: npm-test@1.0.0
npm ERR! notsup Not compatible with your version of node/npm: npm-test@1.0.0
npm ERR! notsup Required: {"node":"14.x"}
npm ERR! notsup Actual:   {"npm":"8.1.2","node":"v16.13.2"}

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/-----/.npm/_logs/2022-10-20T12_55_34_953Z-debug.log
```
## ■　engine-strict=true
パッケージインストール時のプログレスバーを非表示する。

場合によっては 15 秒ほど速くなることもあるらしい。
## ■　save-exact=true
インストールするパッケージのバージョンを固定する。(意外とこれが一番重要かも。)

```
// E オプションをつけることで同じようにインストールが可能である。
npm install axios -E
```

npm config set でパラメータを追加した場合、~/.npmrc ファイルが生成される。

このファイルは、プロジェクトフォルダのルートに配置しても同じ効果を得る事ができた。

実際に試したところ、~/.npmrc の設定値が優先された。

また、ルートの .npmrc にしか設定してない値も適用される模様。

# npm を強制する
Next や Create React App インストール時に ```--use-npm``` オプションをつけることで、

パッケージマネージャーを npm に強制することができる。

[Next公式ドキュメント](https://nextjs.org/docs/api-reference/create-next-app)
```
npx create-next-app@latest --ts --use-npm
```

