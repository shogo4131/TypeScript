# JavaScriptのプリミティブ型について

1. string
2. number
3. boolean
4. null
5. undefined
6. BigInt
7. Symbol

※上記のBigInt、Symbolはほとんど使用しないので深くは触れない。

- BigInt
  - number型で許容できない数値を超えた際に使用する(基本numberでOK)
  - number型で正確に表示できる数字は`9007199254740991 ~ -9007199254740991`らしいです。この範囲外はBigIntを活用。

- Symbbol
  - ユニークで普遍なデータを生成する時に使用する(Vueでは使う所があるらしい)

## nullとundefinedについて

- null
  - 代入すべき値が存在しないため、値がない。明示的に変数が使用できない時に使う。

- undefined
  - 初期化されていない状態の型。暗黙的に使用する。
  
