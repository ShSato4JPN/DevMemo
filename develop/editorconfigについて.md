# editorconfig とは
[EditorConfig](https://editorconfig.org/)

エディタの設定を制御するもの。

例えば、改行コードや文字列の指定。タブ or スペース、etc...。

今回は下の設定値について調査する。

```
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
indent_size = 2
indent_style = space
trim_trailing_whitespace = true
```

## ■　[*]
全てのファイルに editorconfig の設定を適用する
```
[*.py] ⇨ .py のファイルにだけ適用する。

[*.{js,py}] ⇨ .js、.py のファイルにだけ適用する。
```
## ■　root = true
最上位の EditorConfig に記述する
## ■　charset = utf-8
文字コードを utf-8 にする
## ■　end_of_line = lf
改行コードを lf にする
## ■　insert_final_newline = true
すべてのファイルの最後を改行にする
## ■　indent_style　=　space
インデントをスペースで行う
## ■　indent_size = 2
インデントをスペース2つにする
## ■　trim_trailing_whitespace = true
開業も自前にある空白文字を全て取り除く
