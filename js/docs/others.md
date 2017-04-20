# その他

注意点や、知っておいた方が良いことなどを書き連ねます。

## ▼1つ目
```JavaScript
(function() {
   console.info(a)
   var a = 'hogehoge'
   console.info(a)
})()
```

上記コードの実行結果が分かりますか？

* A1: エラー
* A2: 'hogehoge'が2回表示
* A3: 'undefined', 'hogehoge'

答えは__A3__になります。

何が行われているかというと、1つ目の`console.info`では変数`a`が呼ばれていますが、
同スコープ内で`a`という変数があるか確認、あればまだ定義されていないだけですので、内部的に`var a`が呼ばれます。（aという変数の宣言）
なければ外のスコープを探し、最終的にグローバル(`window`)にもいなければエラーとなります。
実際、下記コードはエラーとなります。

```JavaScript
(function() {
   console.info(b)   // <= Uncaught ReferenceError: b is not defined
 })()
```

## ▼2つ目

JavaScriptでは引数の数より多いパラメータを関数に渡してもエラーになりません。

```JavaScript
function hoge(foo, bar) {
   console.info(foo)
   console.info(bar)
   console.info(arguments)   // <= この子が役に立つ
}

hoge('hoge', 'fuga', 'piyo', 123, true)

// 結果
// hoge
// fuga
// ["hoge", "fuga", "piyo", 123, true, callee: function, Symbol(Symbol.iterator): function]
```

上記のように、__`arguments`という配列__に引数が全て保持されています。

## ▼3つ目
JavaScriptにおける変数への代入は、__プリミティブ型は値渡し__、__オブジェクト型は参照渡し__となります。（自分も引っかかりました）

- `プリミティブ型`
  * 数値
  * 文字列
  * ブーリアン
  * null
  * undefined
- `オブジェクト型`
  * 配列
  * 関数
  * オブジェクト

具体的にコードを見てみましょう。

```JavaScript
// プリミティブ型
var a, b
a = 0
b = a
b = 5

console.info(b)   // => 5
console.info(a)   // => 0 aに変化なし

// オブジェクト型1
var hoge = function() {
   console.info('hoge')
}

var fuga = hoge
fuga()   // -> 'hoge'

fuga.foo = 'foo'
hoge.foo   // => 'foo' hogeにもfooが加わる

// オブジェクト型2
var arr1 = [1, 2, 3]
arr2 = arr1
arr2[0] = 5

console.info(arr2)   // => [5,2,3]
console.info(arr1)   // => [5,2,3] arr1も変わる

arr2 = []
console.info(arr2)   // => []
console.info(arr1)   // => [5,2,3] arr1は変わらない
```

## ▼4つ目
丸め誤差についてです。これは以下のコードを実行し、結果を見ていただければ一目瞭然です。

```javascript
var sum = 0,
    num = 0

for (i=0; i<=10; i++) {
   sum += 0.1
   console.log('sum = ' + sum)
}

num = 0.1 * 10
console.log('num = ' + num)
```
