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


