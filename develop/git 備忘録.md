おすすめコマンド
- git log --oneline

git のログを１行で表示する。
コミットID も表示されるので便利

- git ref

git の操作ログを表示する。
何をやったのか一発でわかる。

|||英語|なんとなく適当な日本語訳|
|-|-|-|-|
|p|pick|use commit|コミットを使う|
|r|reword|use commit but edit the commit message|コミットを使うが、コミットメッセージを編集する|
|e|edit|use commit, but stop for amending|コミットを使うが、修正を止める
|s|squash|use commit, but meld into previous commit|コミットを使うが、以前のコミットに混ぜる
|f|fixup|like "squash", but discard this commit's log message|squashと似ているが、コミットメッセージは破棄する
|x|exec|run command (the rest of the line) using shell|シェルを使用して、残りのコマンドを実行する
|d|drop|remove commit|コミットを削除する

■ 参考サイト

https://qiita.com/ykhirao/items/e9f723a553d4eb050817