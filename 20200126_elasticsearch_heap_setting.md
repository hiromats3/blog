## meta

- created: 20200126
- updated: 20200720


# Elasticsearch ヒープサイズ設定

基本的には公式ドキュメントを参照したほうが良い。これは英語を読まずに概要を抑えたいものぐさマン向けの記事。

## 公式ドキュメント

[Setting the heap size](https://www.elastic.co/guide/en/elasticsearch/reference/current/heap-size.html)

## 前提

執筆時のバージョン
- Elasticsaerch 7.6

## ヒープサイズ設定時の考慮事項

- ヒープサイズはjvm.optionsファイルやES_JAVA_OPTSの`Xms`（最小）と`Xmx`（最大）で指定する

- `Xmx`と`Xms`には同じ値を設定する
    - デフォルトでは、最小と最大に1GBのヒープが指定されている

- 適切な設定値はサーバーの物理メモリサイズによって異なる
    - Elasticsearchで使用できるヒープが多いほど、内部キャッシュメモリは多くなるが、OSがファイルキャッシュに使用できるメモリは少なくなる
    - また、ヒープが大きいと、GCによる一時停止時間が長くなる可能性がある

- 物理メモリの50%以下の値を指定する
    - これはJVMヒープ以外の目的で使用するメモリを残すため
    ‐ 例えば、Luceneは物理メモリをファイルキャッシュとして使用する

- 30GB（安全マージンを取るなら26GB）以上指定しない
    - Javaのメモリ使用量が32GBを超えるとポインタのサイズが2倍になり、逆にメモリ使用量が増える（Compressed Oops）ため
