# クロージャ

## ▼説明
名前の通りクローズ（閉じる）者ですが、イメージとしては閉じるというより、__関数を定義した時のスクリーンショット__のイメージの方が近いんじゃないかなと。
一応言語にすると、

#### 「自分を囲むスコープにある変数を参照できる関数」

と表現されることが多いです。誤解を恐れず言うと、全ての関数はクロージャとも言えます。（もちろん例外あり）
スコープの理解も必要ですが、一旦コードを見ていきましょう。

```JavaScript
function func() {
  var value = 1

  // この子がクロージャ
  function innerFunc() {
    console.log(value)
  }
  innerFunc()
}
func() // => 1
```

JavaScriptのスコープの仕様から、上記コードの`innerFunc` という関数内から外にいる `value` という変数が参照できます。（コピーではない点がポイントです）

ちょっと応用した、以下のコードを見てみましょう。

```JavaScript
function func() {
  var value = 0

  // この無名関数がクロージャ
  // returnで関数そのものを返す
  return function () {
    return ++value
  }
}

// このcallは関数へのリファレンスとなる
var call = func()

console.info(call())   // => 1
console.info(call())   // => 2
console.info(call())   // => 3
console.info(func.value)   // => undefined

// console.log(value) ←もちろんこれはエラーになる
```

`func()`はクロージャではないですが、__returnされる子はクロージャ__ですので、この子は変数`value`を参照できます。
したがって、`call()`を実行する度に`value`の値がインクリメントされます。
