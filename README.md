---
marp: true
# dark theme
class: invert
---
<!-- headingDivider: 1 -->

# About this contents

GitHub Pages: [https://inoue-ryoki.github.io/react_basic/](https://inoue-ryoki.github.io/react_basic/)

Repository: [https://github.com/inoue-ryoki/react_basic - GitHub](https://github.com/inoue-ryoki/react_basic)

# Reactの良いところ
- **WEBページの表示が高速に**: ページ全体が更新されず、更新された所のみ変更。
- **コンポーネントベースの設計**: UIを小さな部品（コンポーネント）に分けるので、再利用できる。

# コンポーネント

関数単位でコンポーネント化できる

コンポーネント化したファイル作成
App.jsx
```
export const App = () => {
  return (
    <>
      <h1>Hello World</h1>
      <p>コメント</p>
    </>
  )

};
```

App ってコンポーネント名は頭は大文字と決まってる。ファイル名は小文字でも大丈夫

呼び出し

```
import { App } from "./App";

root.render(
  <StrictMode>
    </ App>
  </StrictMode>
)
```

## コンポーネントに書いてるReact FCとは？

React.FCとはコンポーネントの型定義である。React.FCは、constによる型定義でコンポーネントを定義できる型。

```
const MyTag: React.FC = () => {
  return <div>こんにちは</div>;
};

const Container: React.FC = () => {
  return <MyTag />;
};
```

多分以下のように属性値を使う事が多い？

```
const MyTag: React.FC<{ title: string; }> = (props) => {
  return <div>{props.title}</div>;
};

const Container: React.FC = () => {
  return <MyTag title="こんばんは" />;
};
```

# Props

コンポーネントに渡す引数のようなもの
これを使う事によって、値を柔軟に代入できる。

例

```
import React from 'react';

const Greeting = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

const App = () => {
  return (
    <div>
      <Greeting name="Alice" />
      <Greeting name="Bob" />
    </div>
  );
};

export default App;


```

# State

状態を表す

例
```
import React, { useState } from 'react';  // stateをインポート

export const App = () {
  // countは現在の状態、setCountは状態を更新するための関数
  // 配列の分割代入
  // 初期値は0になる
  const [count, setCount] = useState(0); // 関数の一番上の階層に宣言しないといけない
  const onClickCountUp = () => {
   setCount(count + 1);
   setCount(count + 1); // 二連続で書いても結果は同じ
  };

  return (
    <>
      <button onClick={onClickCountUp}>カウントアップ</button>
      <p>{count}</p>
    </>
  );
}


```

例
```
import React, { useState } from 'react';  // stateをインポート

export const App = () {
  // countは現在の状態、setCountは状態を更新するための関数
  // 配列の分割代入
  // 初期値は0になる
  const [count, setCount] = useState(0); // 関数の一番上の階層に宣言しないといけない
  const onClickCountUp = () => {
   setCount((prev) => prev + 1); //関数を渡すこともできる
   setCount((prev) => prev + 1); // 二連続で書くと二つとも実行される。prevは今のcountの値
  };

  return (
    <>
      <button onClick={onClickCountUp}>カウントアップ</button>
      <p>{count}</p>
    </>
  );
}


```



# useEffect

ReactのuseEffectは、関数コンポーネント内で副作用（side effects）を実行するためのフックです。副作用とは、コンポーネントのレンダリングに直接関係しない処理のことを指します。例えば、データのフェッチ、DOMの操作、サブスクリプションの設定や解除などが含まれます

# カスタムフック

- ただの関数の事
- hooksの各機能を使用
- コンポーネントからロジックを分離
- 使いまわし、テスト容易
- 自由に作れる。use～ という名前にする

例

```
export const useAllUsers = () => {
  const [userProfiles, setUserProfiles] = useState<Array<UserProfile>>([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(false);

  const getUsers = () => {
    setLoading(true);
    setError(false);
    axios
      .get<Array<User>>("https://jsonplaceholder.typicode.com/users")
      .then((res) => {
        const data = res.data.map((user) => ({
          id: user.id,
          name: `${user.name}(${user.username})`,
          email: user.email,
          address: `${user.address.city}${user.address.suite}${user.address.street}`,
        }));
        setUserProfiles(data);
      })
      .catch(() => {
        setError(true);
      })
      .finally(() => {
        setLoading(false);
      });
  };

  return { getUsers, userProfiles, loading, error };
};
```

カスタムフックと普通の関数の違いは、Reactのフック(useState, useEffect)を使用している事。
名前がuse～ から始まる事等
