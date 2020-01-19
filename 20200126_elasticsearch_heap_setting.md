# Elasticsearch ヒープサイズ設定

詳細は公式ドキュメントを見たほうが早い。これは英語を読まずに概要を抑えたいものぐさ向けの記事。

## 公式ドキュメント

[Setting the heap size](https://www.elastic.co/guide/en/elasticsearch/reference/current/heap-size.html)

## 前提

執筆時のバージョン
- Elasticsaerch 7.5

## ヒープサイズの設定時に考慮すること

- ヒープサイズはjvm.optionsファイルやES_JAVA_OPTSの`Xms`（最小）と`Xmx`（最大）で指定する
- `Xmx`と`Xms`には同じ値を設定する
- デフォルトでは、最小と最大に1GBのヒープが指定されている
- 適切な設定値はサーバーのRAMサイズよって異なる
- Elasticsearchで使用できるヒープが多いほど、内部キャッシュメモリは多くなるが、OSがファイルシステムキャッシュに使用できるメモリは少なくなる
- また、ヒープが大きいと、GCによる一時停止時間が長くなる可能性がある
- `Xmx`と`Xms`には物理RAMの50%以下の値を指定する、これはJVMヒープ以外の目的で使用するメモリを残すため
- `Xmx`と`Xms`を、JVMが圧縮oopsに使用するしきい値以下に指定する。理想的にはゼロベース圧縮oopsのしきい値以下にする
    - この項目は正直理解できなかったが、概ね26GB以下とするのが安全なよう