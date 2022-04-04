# ユーティリティタイプについて

### ReadOnly

読み取り専用となる。valueの値まで固定したい場合は、cosntアサーションを使用する方がいい。

```
type User = {
  name: string,
  age: number,
  sex?: male | womon
}

const user: Readonly<User> = {
  name: 'taro',
  age: 24,
}
 
user.age = 30 × エラー
```

### Partial

全てオプショナルにできる。型が緩くなるので使用には注意が必要。

```
type User = {
  name: string,
  age: number,
}

type OptionalUser = {
  firstName: string,
  lastName: string,
  country: 'Japan' | 'Korean'
}

type UserInfo = Partial<OptionalUser>;

const user: UserInfo = {
  name: 'taro',
  age: 24,
  country: 'Japan' // あってもなくてもOK
}
```

### Required

オプショナルの反対で全て必須である。

```
Reactでの例

type InputType = Required<Pick<ComponentProps<'input'>, 'name' | 'placeholder'>>;

上記は、input要素のname、placeholderを抜き出し、必須にすることで下記の様な型を生成できる。

type InputType = {
   name: string;
   placeholder: string;
}
```

### Pick

必要な型を抜き出す。

```
type User = {
  name: string,
  age: number,
  sex?: male | womon
}

const userName: Pick<User, 'name'> = {
  name: 'taro',
  age: 25 // ×エラー
}
```

### Omit

不要な型を除外する。
ReactではComponentPropsと一緒に使用されることが多い。

```
classNameを除外してsytleをオーバーライドできる様にする。

type Props = Omit<React.ComponentProps<'input'>, 'className'>

export const Input = (className: string, props: Props) => (
  <input
    {...props} // <- className は含まれない（型エラーで事前に弾かれる）
    className={clsx(styles.input, className)} // clsxなどでデフォルトのstyleを上書きできる
  />
)
```

### Extract

第一引数と、第二引数で指定した物で互換性のある型を抽出する。
オブジェクトはkeyを取得したら可能。
これUnion型で必要なものだけ抽出できるから神じゃね？？

```
type Test = Extract<string | number, string>

// Testはstring型になる
```

　stringリテラルタイプやnumberリテラルタイプでもstring、numberと互換性があるので使用できる。

```
type Test = Extract<'test' | number, string>

// Testは'test'(string literal typesになる)

type Test = Extract<string | 100, number>

// Testは100(number literal typesになる)

```

互換性のない値を設定するとnever型になる。

```
type Test = Extract<string | 100, boolean>

// Testはnever型になる
```

### Exclude

Extractの逆。第一引数と第二引数が合致しないものを返す。

```
// union型で不要な物を除いた型を作成できたりする

type Size = 'small' | 'normal' | 'large' | 'medium'

// 第二引数をtypoすると除外されないので注意が必要。
type BoxSize = Exclude<Size, 'small'>

```

### Record

オブジェクトのkeyとvalueを指定できる。

```
type Page = {
  url: string
  authorized: boolean
};

type Params = 'login' | 'logout'

type Pages = Record<Params, Page>

const page :Pages = {
  login: {
    url: 'login',
    authorized: false
  },
  logout: {
    url: 'logout',
    authorized: true
  }
}

```

### Parameters


