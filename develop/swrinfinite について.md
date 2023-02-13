簡単にメモ。

"swr/infinite"、"react-infinite-scroll-component" を使った無限スクロールを実装した。

実装時にかなりハマったところがあったので後学のためにメモ。

- fetcher で取得するデータの型
    fetcher のレスポンスデータはどうも配列データでないとうまく動かない模様。。。

    変な型になっていると getKey の引数（previousData） にデータが格納されず

    pageIndex がカウントアップされずデータが取得されない。かなりハマった。
