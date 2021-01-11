# クロージャ

## ▼説明
名前の通りクローズ（閉じる）者ですが、イメージとしては閉じるというより、__関数を定義した時のスクリーンショット__のイメージの方が近いんじゃないかなと。
一応言語にすると、

#### 「自分を囲むスコープにある変数を参照できる関数」

と表現されることが多いです。誤解を恐れず言うと、全ての関数はクロージャとも言えます。（もちろん例外あり）
スコープの理解も必要ですが、一旦コードを見ていきましょう。

```js
const func = () => {
  const value = 1

  // この子がクロージャ
  const innerFunc = () => {
    console.log(value)
  }
  innerFunc()
}
func() // => 1
```

JavaScript のスコープの仕様から、上記コードの `innerFunc` という関数内から外にいる `value` という変数が参照できます。（コピーではない点がポイントです）

ちょっと応用した、以下のコードを見てみましょう。

```js
const func = () => {
  let value = 0

  // この無名関数がクロージャ
  // returnで関数そのものを返す
  return () =>  ++value
}

// このcallは関数へのリファレンスとなる
const call = func()

console.info(call())   // => 1
console.info(call())   // => 2
console.info(call())   // => 3
console.info(func.value)   // => undefined

// console.log(value) ←もちろんこれはエラーになる
```

`func()` はクロージャではないですが、__`return` される子はクロージャ__ですので、この子は変数`value`を参照できます。
したがって、`call()` を実行する度に `value` の値がインクリメントされます。
