# TypeScriptの型

※自分が理解不足だった所だけPick Up

- Tuple
- Unknown
- Never
- Void

### Tuple型

配列の順番に型を使用できる。

```
サンプル

const test: [string, number, boolean] = ['test', 100, false];

Error
const test: [string, number, boolean] = ['test', 100];     // booleanを指定していないとエラーになる
const test: [string, number, boolean] = ['test', 100, '']; // 二番目の要素にはbooleanしか指定できない

```

可変調Tuple型もあるらしい、、
最初の二つは絶対に指定しないといけないが、それ以降はstring型のみあってもなくても良い。

```
サンプル

OK
const test:[string, number, ...string[]] = ['test', 100, ''];
const test:[string, number, ...string[]] = ['test', 100];

NG
const test:[string, number, ...string[]] = ['test', 100, false]; // エラー
```

配列の戻り値が決まっていれば使用できそうね、、

### Never型

存在しない値がnever型になる。

```
サンプル1

const test = (): never => {
  throw new Error('error')
} // 値が返らないものはnever型になる
```

```
サンプル2

const test = (num: 1 | 2) => {
  swich (num)
    case: 1:
      return;
    case: 2:
      return
    default:
      num    // この場合絶対にdefaultには届かないのでnever型になる
      break;
 };

```
