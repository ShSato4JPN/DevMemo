# ■ 　 Pick 関数の使い所

例えば、swr と　 useMemo を利用する時、

```
onst data = await getEntries();
  const value = useMemo(
    () => ({ fallbackData: data }),
    [data]
  );

  return (
    <div>
      <SWRConfig value={value}> // ERROR !!
        <BlogTop />
      </SWRConfig>
    </div>
  );
```

value にフェッチしたデータを fallbackData して渡してもエラーとなる。

```
<SWRConfig value={value}> // ERROR !!
```

理由は簡単で、`getEntries` の返却値（value）の型が `SWRConfig` の value の fallbackData）の型と異なっているから。

そこで、`const value` の型を `SWRConfig` の型に合わせる作業を行う。

まずは `SWRConfig` の value の fallbackData）の型を調べる。

```
eclare const SWRConfig: react.FC<react.PropsWithChildren<{
    value?: (Partial<swr__internal.PublicConfiguration<any, any, swr__internal.BareFetcher<any>>> & Partial<swr__internal.ProviderConfiguration> & {
        provider?: ((cache: Readonly<swr__internal.Cache<any>>) => swr__internal.Cache<any>) | undefined;
    }) | ((parentConfig?: (Partial<swr__internal.PublicConfiguration<any, any, swr__internal.BareFetcher<any>>> & Partial<swr__internal.ProviderConfiguration> & {
        provider?: ((cache: Readonly<swr__internal.Cache<any>>) => swr__internal.Cache<any>) | undefined;
    }) | undefined) => Partial<swr__internal.PublicConfiguration<any, any, swr__internal.BareFetcher<any>>> & Partial<swr__internal.ProviderConfiguration> & {
        provider?: ((cache: Readonly<swr__internal.Cache<any>>) => swr__internal.Cache<any>) | undefined;
    }) | undefined;
}>> & {
    defaultValue: FullConfiguration;
};
```

一見ごちゃごちゃしているように見えるが、意味さえわかればどうってことない。

`Partial` は、ジェネリクスで渡した型全てにオプションプロパティを付与するものである。

> ※ オプションプロパティとは、`test?: string` のようなもので、定義しなくても問題ない型を宣言することができる。

つまりは、こちらの型がベースとなる。

```
PublicConfiguration
```

なので、useMemo にジェネリクスを設定する。

```
const value = useMemo<PublicConfiguration>(
    () => ({ fallbackData: data }),
    [data]
  );
```

次に、`PublicConfiguration` の定義を確認する。

```
interface PublicConfiguration<Data = any, Error = any, Fn extends Fetcher = BareFetcher> {
    errorRetryInterval: number;
    errorRetryCount?: number;
    loadingTimeout: number;
    focusThrottleInterval: number;
    dedupingInterval: number;
    refreshInterval?: number | ((latestData: Data | undefined) => number);
    refreshWhenHidden?: boolean;
    refreshWhenOffline?: boolean;
    revalidateOnFocus: boolean;
    revalidateOnReconnect: boolean;
    revalidateOnMount?: boolean;
    revalidateIfStale: boolean;
    shouldRetryOnError: boolean | ((err: Error) => boolean);
    keepPreviousData?: boolean;
    suspense?: boolean;
    fallbackData?: Data;
    fetcher?: Fn;
    use?: Middleware[];
    fallback: {
        [key: string]: any;
    };
    isPaused: () => boolean;
    onLoadingSlow: (key: string, config: Readonly<PublicConfiguration<Data, Error, Fn>>) => void;
    onSuccess: (data: Data, key: string, config: Readonly<PublicConfiguration<Data, Error, Fn>>) => void;
    onError: (err: Error, key: string, config: Readonly<PublicConfiguration<Data, Error, Fn>>) => void;
    onErrorRetry: (err: Error, key: string, config: Readonly<PublicConfiguration<Data, Error, Fn>>, revalidate: Revalidator, revalidateOpts: Required<RevalidatorOptions>) => void;
    onDiscarded: (key: string) => void;
    compare: (a: Data | undefined, b: Data | undefined) => boolean;
    isOnline: () => boolean;
    isVisible: () => boolean;
}
```

今回使用したいのは `fallbackData?: Data;` のみ。

なのに、オプションプロパティが付与されていない型が結構な数あるため実装が非常に厄介である。

そんな時に、`Pick` を使う。`Pick` を使うことで特定の方だけを抽出することができる。

```
const value = useMemo<Pick<PublicConfiguration, "fallbackData">>(
    () => ({ fallbackData: data }),
    [data]
  );
```

で、最後に `PublicConfiguration` にジェネリクスを設定することで完成。

```
  const data = await getEntries();
  const value = useMemo<Pick<PublicConfiguration<typeof data>, "fallbackData">>(
    () => ({ fallbackData: data }),
    [data]
  );
```

`typeof 〇〇`　を使うことで変数の型を取得するとができる。

非常にスマートである。

---

Pick, Pertial 例

```
export type hoge = {
  name: string;
  age: number;
  blood: string;
  sex: string;
};

const satoshi: hoge = {
  name: "satoshi",
  age: 28,
  blood: "ab",
  sex: "man",
};

const foo: Pick<hoge, "name"> = {
  name: "satoshi",
  //age: 28, ERROR
  //blood: "ab", ERROR
  //sex: "man", ERROR
};

const bar: Partial<hoge> = {}; // NO ERROR

```
