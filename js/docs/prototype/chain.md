# プロトタイプチェーン

## ▼説明
まずは以下のコードを見て下さい。

```JavaScript
// 関数を定義
let hello = function () {}

// 中身を確認
console.dir(hello)

// こんな感じ
function hello()
   arguments: null
   caller: null
   length: 0
   name: "hello"
   prototype: Object   // ←この子と
   __proto__: ()   // ←この子がポイント
   [[FunctionLocation]]: VM701:2
   [[Scopes]]: Scopes[1]
```

`prototype` は置いておいて、 `__proto__`について。
この子は誰かというと、__`Function`コンストラクタの`prototype`__オブジェクトでした。

```JavaScript
hello.__proto__ === Function.prototype   // => true

// ちなみに
Function.__proto__ === Object.__proto__   // => true
```

（ここからが今回の内容）

では、`Function`コンストラクタの`prototype`オブジェクトに`hoge`プロパティを追加し、`hello`（オブジェクト）からアクセスしてみましょう。

```JavaScript
// hogeという名前のオブジェクトプロパティを追加
Function.prototype.hoge = {name: 'hoge'}

// hogeプロパティにアクセス
hello.hoge   // => Object {name: "hoge"}
```

改めて`hello`の中身を見てみましょう。
しかし、`hoge`というプロパティは存在しないはずです。

そこで、`prototype`と`__proto__`の中身を見てみましょう。

```JavaScript
// 再度中身を確認
console.dir(hello)

/** prototype **/
console.dir(hello.prototype)

// こんな感じ
Object
   constructor: ()
   __proto__: Object

// つまり、prototypeオブジェクトにもいないと。次。


/** __proto__ **/
console.dir(hello.__proto__)

// こんな感じ
function anonymous()
   （中略）
   constructor: Function()
   hoge: Object   // ←いたー!!!!
   length: 0
   name: ""
   toString: toString()
   （中略）
   __proto__: Object
   [[FunctionLocation]]: <unknown>
```

上記から、`hoge`プロパティは`hello.__proto__`の中にいることがわかりました。ここで一つ疑問が。

* Q: `hello.__proto__.hoge`でアクセスするんじゃないの？
* A: それは直接的なアクセスの仕方で、 `hello.hoge`でもOK。それが__プロトタイプチェーン__。

JavaScriptでは、オブジェクトのプロパティにアクセスする際は、

  1. まずは__対象のオブジェクト__のプロパティを探す
  2. 見つからなければ、対象のオブジェクトの__`prototype`オブジェクト__を探す
  3. 見つからなければ、対象のオブジェクトの__コンストラクタの`prototype`オブジェクト__を探す
  4. 見つからなければ、__`Object`コンストラクタの`prototype`オブジェクト__を探す
  5. 見つからなければ`undefined`を返す

というように、`__proto__`を（もっと言うと、基のオブジェクトの`prototype`を）追って探します。これを__プロトタイプチェーン__といいます。
最後に、この`hoge`プロパティには__新たなオブジェクトからもアクセスが可能__となります。

```JavaScript
/**
 * Functionコンストラクタのprototypeオブジェクトに
 * hogeプロパティを追加済み
 */
var bye = function(){}
var foo = new Function()

bye.hoge   // => Object {name: "hoge"}
foo.hoge   // => Object {name: "hoge"}

// ObjectコンストラクタのtoStringメソッドも呼べる
foo.toString   // => function toString() { [native code] }
```