# Literal Typeについて

TypeScriptではプリミティブ型の特定の値だけを代入可能にする型をリテラル型という。

```
サンプル

const name: taro = "taro"
const num: 0 = 0
const bool: true = false × エラー
```

上記の場合はnameにはtaro,numには0,boolにはtrueしか代入できない。
単体では使用することはあまりないが、ユニオン型で結合して使用することは頻度が多い。

```
サンプル

type Name = 'jon' | 'taro' | 'sato';

const name: Name = 'jon'; ○
const name: Name = 'aki'; × エラー
```

## constとletの挙動の違い

constで定義したものはstring literal typeだが、letへ再代入すると元の型に拡張されてしまう。(今回の場合はstring型になる)

letは再代入できるものなので、literal typeで固定できない？？

```
サンプル

const name = 'taro' // string literal typeのまま
let name2 = name    // string型
```

しかし、literal typeを維持したい場合もあるだろう、、、

```
サンプル

1. const name: 'taro' = 'taro';
2. const name = 'taro' as 'taro';  // asは冗長だし無理やり使用したらバグを引き起こす可能性大
3. const name = 'taro' as const;   // 2よりはconst アサーションを使用する方がいい

let name2 = name;  // literal typeのまま代入することができる
```

個人的にはconstアサーション or 型注釈でしっかり型を固定した方がバグを防げると感じた。
