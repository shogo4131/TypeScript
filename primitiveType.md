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
  - 代入すべき値が存在しないため、値がない。現在利用できない値。

``` 
サンプル

let a = null 
```

nullは自動的に発生しないので、開発者が上記のように値が入っていないことを明示的に示すことになる。


- undefined
  - 初期化されていない状態の型。暗黙的に使用する。

```
サンプル

let a;
```

この場合は、変数の初期化を行っていないので```undefined``` になる。

### null vs undefined

[TypeScript公式](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines#:~:text=null%20and%20undefined,not%20use%20null.)ではnullは使用せずにundefinedを使用することを推奨している。
しかし、APIの返り値でnullが返ってくる時もあるのでnullを絶対に使わないということは出来なさそう。。

### 厳密等価演算子(===)と等価演算子(==)

```
null === undefined   // false
null  == undefined   // true
```
詳しい内容は書かないが。等価演算子を使用した場合nullとundefinedが等しい判定になってしまうのでJavaScript(TypeScript)では厳密等価演算子のみ使用した方がいい。




  
