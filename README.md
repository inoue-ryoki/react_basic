---
marp: true
# dark theme
class: invert
---
<!-- headingDivider: 1 -->

# About this contents

GitHub Pages: [https://inoue-ryoki.github.io/sample_marp/](https://inoue-ryoki.github.io/react_basic/)

Repository: [https://github.com/inoue-ryoki/sample_marp - GitHub](https://github.com/inoue-ryoki/react_basic)

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

# Props

コンポーネントに渡す引数のようなもの

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
